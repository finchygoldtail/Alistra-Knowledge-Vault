---
title: Concurrent Login Control
type: security
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [security, auth]
---

# Concurrent Login Control

Built 2026-08-07 to stop shared logins bypassing licence seat limits ("one user at one time" — someone else signing in on the same credentials silently signs the first device out).

## Mechanism

- A `activeSessionToken`/`activeSessionStartedAt` pair is stamped onto the user's `businesses/{businessId}/users/{uid}` profile doc by a new callable, `stampUserSession`, called by the client **only immediately after a genuine sign-in action** (email/password, Google popup, or completed TOTP MFA) — never on page-refresh or `onAuthStateChanged` resume. Getting that distinction wrong would make every new tab of the same login kick every other tab of the same login, the opposite of the intended behaviour.
- The token is stored in `localStorage` (shared across tabs of the same origin, so a second tab of the same login doesn't mint a second token or trigger a kick).
- A Firestore `onSnapshot` listener on the profile doc (`useSessionEnforcement` hook) compares the local token against the live remote value on every snapshot and silently signs the tab out on mismatch.
- Admin and Super Admin roles are exempt.
- Fails open on listener errors (network blip on a field tablet must never spuriously log someone out) — `admin.auth().revokeRefreshTokens(uid)` is called as defense-in-depth on every fresh sign-in, but does **not** by itself achieve an instant kick, since an already-issued ID token stays valid client-side until its natural refresh. The `onSnapshot` listener is what actually delivers the kick.

## Bug found and fixed in code review (2026-08-07)

The listener originally read its local comparison token once, at mount. Because `stampUserSession` resolves over the network, on a fresh sign-in the listener almost always mounted and read a still-empty token *before* the callable had written it to `localStorage`, bailed out, and never subscribed at all — silently defeating the feature for the most common case (the device that had just signed in was never protected against a later sign-in elsewhere). Fixed by reading the local token fresh inside every snapshot callback instead of once at mount, so the listener always attaches promptly and still catches a token that lands slightly late.

## Related

- [[Authentication]]
- [[Audit Logging]]
- [[API Security]]
- [[Role Matrix]]

