---
title: Authentication
type: architecture
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-08
tags: [auth, firebase]
---

# Authentication

AlistraGIS uses Firebase Authentication with Google and email authentication.

## Requirements

- Support Google sign-in and email sign-in.
- Connect authenticated users to company and project access in [[Permissions Model]].
- Support future login restrictions in [[Concurrent Login Control]].

## Actual implemented model (Stage 8 review, 2026-08-08)

This section replaces the requirements-only framing above with what `fibre-gis`'s `AuthGate.tsx` and `useSessionEnforcement.ts` actually do today — the requirements above were all met and substantially exceeded before this review, they just weren't documented.

- **Sign-in methods**: email/password (`signInWithEmailAndPassword`) and Google (`signInWithPopup`). Both routes handle Firebase's `auth/multi-factor-auth-required` response by prompting for a TOTP code before completing sign-in.
- **MFA is mandatory, not optional, for every account.** After a successful sign-in (and after any forced password change resolves), any account without an enrolled TOTP factor is shown a full-screen, non-dismissable setup modal (QR code + manual key, via Google Authenticator or equivalent) before the app renders. There is no skip/remind-later option — the only alternative to enrolling is signing out. This is a materially stronger posture than most SaaS products, which treat MFA as opt-in.
- **Email verification is enforced** before the app renders — an unverified account sees a verification gate (resend + "I've verified" recheck), not the product.
- **Password reset**: standard Firebase `sendPasswordResetEmail` flow, self-service from the login screen.
- **Forced password change**: an admin can flag a profile with `forcePasswordChange: true`; the next sign-in shows a mandatory change-password modal (8+ characters, enforced both client-side and again server-side in the `changeOwnPassword` callable) before anything else renders, then signs the user out to force a clean re-login with the new credential.
- **Account disabling**: every membership document carries `active` (default true); `isActive()` is checked everywhere role/permission is resolved (Firestore rules and every Cloud Function), so setting `active: false` immediately revokes access without needing to touch Firebase Auth itself.
- **Account recovery beyond self-service reset**: none beyond standard Firebase password reset — there's no documented "locked out, contact support" operational process yet. Worth covering in Stage 8's eventual `Support/Ticketing` build-out (Stage 28).
- **Session expiry / concurrent sessions**: see [[Concurrent Login Control]] for the full mechanism — a `stampUserSession` callable stamps a fresh session token on genuine sign-in; a Firestore listener (`useSessionEnforcement`) compares the locally-held token against the profile doc's token and signs the tab out the moment a second sign-in overwrites it elsewhere. Deliberately **fails open** on listener errors (a network blip on a field tablet must never spuriously log someone out) — `revokeRefreshTokens` server-side is the actual backstop for when fail-open matters.
- **Privileged-account note (relevant to this stage's "implement stronger protection for Super Admin/Admin" instruction):** `useSessionEnforcement` explicitly **exempts** `admin` and `super_admin` roles from the single-session kick-out — i.e. the highest-privilege accounts currently get *weaker* session-concurrency enforcement than everyone else, not stronger. This may be a deliberate, reasonable tradeoff (support/ops staff plausibly need legitimate multi-device access), but it's the opposite of what this stage asked to check for, so flagging it explicitly rather than silently accepting it: **worth an explicit product decision** on whether privileged accounts should get the same or *stricter* concurrent-session enforcement, not an exemption from it. No code change made — this is a policy call, not a bug.
- **Platform-owner bootstrap**: a hardcoded owner-email allow-list (`OWNER_EMAILS`) grants implicit `super_admin` regardless of any Firestore document, independently evaluated in five separate places across the codebase (Firestore rules, Storage rules, and three places in `functions/src`). Already flagged in [[Secrets Audit 2026-08-08]] and the original current-state validation as undocumented/duplicated; no single source of truth. Not fixed this session (out of scope for an authentication *review* — this is a consolidation refactor, not a vulnerability, since all five copies currently agree).

## Not reviewed in this pass

Firebase Auth's own built-in abuse protections (rate-limiting repeated failed sign-in attempts, temporary account lockouts) are platform-level and were not independently verified — they're Google's responsibility, not app code, so there's nothing in this repo to audit for them.

