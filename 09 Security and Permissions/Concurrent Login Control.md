---
title: Concurrent Login Control
type: security
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-20
tags: [security, auth]
---

# Concurrent Login Control

Built 2026-08-07 to stop shared logins bypassing licence seat limits ("one user at one time" — someone else signing in on the same credentials silently signs the first device out).

## Mechanism

- A `activeSessionToken`/`activeSessionStartedAt` pair is stamped onto the user's `businesses/{businessId}/users/{uid}` profile doc by a new callable, `stampUserSession`, called by the client **only immediately after a genuine sign-in action** (email/password, Google popup, or completed TOTP MFA) — never on page-refresh or `onAuthStateChanged` resume. Getting that distinction wrong would make every new tab of the same login kick every other tab of the same login, the opposite of the intended behaviour.
- The token is stored in `localStorage` (shared across tabs of the same origin, so a second tab of the same login doesn't mint a second token or trigger a kick).
- A Firestore `onSnapshot` listener on the profile doc (`useSessionEnforcement` hook) compares the local token against the live remote value on every snapshot and silently signs the tab out on mismatch.
- **Applies to every role.** Admin and Super Admin used to be exempt; that was removed on 2026-08-20 — see below.
- Fails open on listener errors (network blip on a field tablet must never spuriously log someone out). The `onSnapshot` listener is what actually delivers the kick.
- `admin.auth().revokeRefreshTokens(uid)` **was** called as defense-in-depth on every fresh sign-in. It was removed on 2026-08-19 after it was found to be signing every user out on their first page refresh — see below. Enforcement is unaffected; the token comparison was always what did the work.

## Bug found and fixed in code review (2026-08-07)

The listener originally read its local comparison token once, at mount. Because `stampUserSession` resolves over the network, on a fresh sign-in the listener almost always mounted and read a still-empty token *before* the callable had written it to `localStorage`, bailed out, and never subscribed at all — silently defeating the feature for the most common case (the device that had just signed in was never protected against a later sign-in elsewhere). Fixed by reading the local token fresh inside every snapshot callback instead of once at mount, so the listener always attaches promptly and still catches a token that lands slightly late.

## Bug found and fixed in production (2026-08-19)

The defense-in-depth `revokeRefreshTokens` call was signing **every user, on every role, out on their first page refresh**. Reported as "I refresh and it logs me straight out", including when signed in as Super Admin.

`revokeRefreshTokens` is a per-uid operation. There is no way to revoke every session except the caller's own, so calling it inside `stampUserSession` — which runs immediately after a genuine sign-in — invalidated the token that same sign-in had been issued seconds earlier. The already-issued ID token stayed valid for the rest of its hour, which hid the fault until the next page load, when the SDK revalidated the persisted user, received `400 TOKEN_EXPIRED` from `accounts:lookup`, and cleared the session.

Two things made it hard to spot. It only surfaced on refresh, not at sign-in, so it looked like a persistence problem rather than a revocation one. And because the revoke ran server-side, it ignored the Admin/Super Admin exemption in `useSessionEnforcement` entirely — the natural diagnostic step of signing in as a privileged account did not rule the mechanism out, it just produced the same symptom.

It also never achieved what it was added for: being per-uid, it killed the newly created session alongside the old one, rather than just the old one.

Fixed by removing the call. Reproduced against the emulator beforehand (`accounts:lookup` returning 400 immediately after stamping), and re-verified after: `accounts:lookup` returns 200, a second sign-in still rotates `activeSessionToken`, the older session is still signed out, and the current session survives a refresh. Deployed to `fibre-gis-v2` as a single-function deploy; committed on `fix/session-signout-on-refresh` (`b87e84e`).

If a server-side backstop is wanted again it belongs in a `beforeSignIn` blocking function, which runs before the new token is minted and can therefore revoke prior sessions without destroying the one being created. A code comment in `sessionCallables.ts` records this so the call is not reinstated in the same place.

## Role exemption removed (2026-08-20)

`isExempt = role === "admin" || role === "super_admin"` meant the two highest-privilege roles skipped enforcement entirely, while a manager was signed out for exactly the same behaviour. The accounts most worth protecting had the weakest guarantee.

Flagged twice before it was changed — once in the 2026-08-08 Stage 8 review, and again on 2026-08-19 when it actively obstructed diagnosis of the sign-out bug above: signing in as Super Admin to test produced the identical symptom, so the exemption did not rule the mechanism out.

Removed rather than set to false. `shouldForceSignOut` no longer takes an `isExempt` argument and `useSessionEnforcement` no longer takes a `role`, so no boolean remains that can silently disable the check for a class of account. If sessions ever need to coexist legitimately, that should key on something earned per session — a registered device — not on privilege level.

Verified against the emulator rather than only in unit tests: signed in as `admin` with matching tokens, overwrote `activeSessionToken` as a second device would, and the session terminated in 815ms with the local token cleared and the app torn down. The replaced unit test asserted the opposite ("never kicks an exempt role, even on mismatch"), so this is a genuine before/after.

Deployed via Vercel (`81a1cde`, production, READY).

**Operational consequence:** an admin or super_admin signed in on a laptop and a tablet will now have the older session terminated when they sign in on the other. This is intended, but it is new behaviour for those roles and worth telling affected people about.

## Related

- [[Authentication]]
- [[Audit Logging]]
- [[API Security]]
- [[Role Matrix]]

