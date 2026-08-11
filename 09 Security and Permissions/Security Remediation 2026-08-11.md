---
title: Security Remediation 2026-08-11
type: security-assessment
status: deployed
owner: Alistair
created: 2026-08-11
updated: 2026-08-11
tags: [security, authentication, multi-tenant, firebase, deployment]
---

# Security Remediation 2026-08-11

## Outcome

An adversarial review of the production website and `fibre-gis` repository identified two Critical and five High-impact security weaknesses. All identified issues were fixed, regression-tested, committed as `eeeab79` (`Harden tenant authentication and storage security`), pushed to GitHub `main`, and deployed to Vercel and Firebase project `fibre-gis-v2` on 2026-08-11.

## Findings closed

1. **Existing-account reset through user creation — Critical.** `createLoginUser` previously updated the password, display name and disabled state when an email already existed. It now creates only new Auth identities and returns `already-exists` without changing credentials or account state. Platform-owner accounts are protected from tenant-admin creation or reassignment.
2. **Cross-tenant administrator escalation — Critical.** A root `admin` profile could previously manage users in a different tenant. Tenant authority now requires an explicitly active membership in the requested business. Cross-tenant authority is limited to the platform owner or an explicitly active root `super_admin`.
3. **Password-change membership creation — High.** `changeOwnPassword` accepted a caller-selected business and could create membership/profile stubs. It now requires a recent authentication event, an existing explicitly-active membership, a non-disabled Auth account and a 12-character password; it updates existing profiles only and revokes refresh tokens.
4. **Inactive and revoked Storage access — High.** Backend Storage authorization now requires explicit `active: true`, rejects disabled Auth accounts and checks revocation state. The HTTP API verifies ID tokens with revocation checking enabled.
5. **Direct `storageProfiles` access — High.** The collection is now explicitly server-managed and denied by Firestore rules rather than falling through to the generic active-member rule.
6. **Script-capable image uploads — High.** Storage rules no longer accept every `image/*` MIME type. JPEG, PNG, WebP, GIF, HEIC and HEIF are allowed; SVG is rejected.
7. **Known vulnerable dependencies and missing response hardening — High.** The frontend and Functions dependency trees were updated and overridden where required. Production npm audits reported zero known production vulnerabilities. Vercel and Firebase hosting configurations now include CSP, HSTS, MIME-sniffing, framing, referrer, permissions and opener-policy headers.

## Verification evidence

- Application/security tests: **277 passed** in the reviewed working tree, including eight dedicated authorization-policy regressions.
- Component tests: **13 passed** across four files.
- Firestore and Storage emulator rules tests: **33 passed**.
- Frontend production build, Functions TypeScript build and repository typecheck: **passed**.
- Production dependency audits: **0 known vulnerabilities** in both frontend and Functions production trees at deployment time.
- Clean release checkout: frontend and Functions builds passed. One unrelated source-text test remained line-ending-sensitive in the Windows checkout; it expects a literal LF sequence and is not a runtime or security failure.
- Vercel combined commit status for `eeeab79`: **success**.
- Live smoke check: `https://alistragis.com/` served `/assets/index-BrwuoPL3.js`, rendered the production landing page, and produced no browser console warnings or errors.
- Firebase: Firestore rules and Storage rules compiled and released; all 128 application Functions completed update after automatic quota retries. Existing `fridayAiHealth` and `fridayChat` functions were preserved.

## Operational implications

- Legacy membership documents without `active: true` now fail closed. If a legitimate historical user cannot sign in, an authorised administrator must review and explicitly activate the correct tenant membership rather than weakening the rule.
- Forced password changes require the user to have authenticated within the preceding five minutes. A stale session must sign in again.
- Existing-email onboarding must use an explicit invitation/membership workflow; the create-login route will not take ownership of an existing Auth identity.
- The known broader product decisions in [[Active Bugs]] remain separate: serverless rate limiting and per-record ownership/read isolation were not silently redesigned in this remediation.

## Related notes

- [[Authentication]]
- [[Role Matrix]]
- [[API Security]]
- [[Vercel Deployment]]
- [[Firebase Infrastructure]]
