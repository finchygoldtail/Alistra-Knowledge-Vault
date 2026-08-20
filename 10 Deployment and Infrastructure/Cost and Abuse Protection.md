---
status: live
updated: 2026-08-21
related: ["[[Decision Log]]", "[[FRIDAY Security Model]]", "[[API Security Assessment 2026-08-08]]", "[[API Security]]", "[[Data Retention Schedule]]"]
---

# Cost and Abuse Protection

Stage 11 of the commercial go-live programme, reviewed 2026-08-08 against fibre-gis.

## What was already in place before this review

- **FRIDAY/NVIDIA calls**: hard zero-cost guard (`isPaidAiAllowed()` defaults `false`, no paid code path exists), per-user rate limiting via a Firestore transaction (`fridayRateLimits`, made server-write-only in the Stage 4 rules fix), request/response size caps, request timeout, no automatic retry on failure (so a failing call surfaces immediately instead of silently burning through the free-tier allowance). See [[FRIDAY Security Model]] for the full picture.
- **Storage**: file size caps enforced in `storage.rules` (25MB for general asset uploads, 10MB for photos) and content-type allowlists — reviewed in Stage 5/3.
- **Bulk operation caps**: bulk employee/vehicle/plant-equipment upserts capped at 500 rows per call; joint-mapping row imports capped at 10,000 rows; `loadAssetChangeLogs`/similar list reads clamp `maxResults` to a 1–100 range.
- **Login attempts**: Firebase Auth's own built-in abuse protection (rate-limiting repeated failed sign-ins) — platform-level, not app code, not independently verified but not this app's responsibility to implement.

## Gap found and fixed: no cap on Cloud Function horizontal scaling

None of the 124 Cloud Functions in the codebase set a `maxInstances` limit, and no project-wide default was configured either (`setGlobalOptions` was never called). Firebase/Cloud Run's default autoscaling is effectively unbounded — a bug causing a retry storm, or a scripted actor hammering any single endpoint, could scale instances (and the bill) far past any realistic traffic level with nothing to stop it.

**Fixed**: added `setGlobalOptions({ maxInstances: 50 })` at the top of `functions/src/index.ts`, positioned to run before any function definitions are evaluated (verified in the compiled CommonJS output, not just assumed from source order — this matters because `export { X } from "./file"` re-exports compile to `require()` calls that execute in source order, so the global-options call has to come first or the other files' functions would already be defined before picking up the default). 50 concurrent instances per function is well above any plausible legitimate concurrent load for this business today — a safety ceiling, not a real-world throttle. Verified with a clean build; **not yet deployed**.

## Closed 2026-08-20/21: App Check and per-user rate limiting

Both gaps flagged above are now closed and deployed.

### App Check — shipped 2026-08-20, live, **not enforced**

Clients attach a reCAPTCHA Enterprise attestation to every request. Wiring is
in `src/appCheck.ts`; the site key is the Vercel production environment
variable `VITE_FIREBASE_APPCHECK_SITE_KEY`. Verified against the deployed
bundle rather than the build output — the key is in the entry chunk and the SDK
in `assets/vendor-firebase-*.js`. Without a key the provider tree-shakes out
entirely, so an unconfigured build behaves exactly as before.

Staged deliberately, because the note above was right that misconfiguring it
locks out real users:

1. ✅ Clients send tokens. Nothing is enforced, so nothing can break.
2. ⏳ Watch Firebase console → App Check → APIs until verified requests reach
   ~100% and hold for several days.
3. ⬜ Only then enable enforcement, one service at a time.

Nothing in the codebase can turn enforcement on. It is a console setting, and
the functions would additionally need `enforceAppCheck: true` on each `onCall`,
which is **not** added — deliberately, so stage 3 stays a conscious act.

**CSP requirement, learned the hard way on 2026-08-21.** App Check loads
reCAPTCHA Enterprise from `https://www.google.com/recaptcha/enterprise.js`.
The CSP in `vercel.json` and `firebase.json` allowed `apis.google.com` and
`www.gstatic.com` but not `www.google.com`, so the script was blocked and the
live login page crawled, with the Google sign-in popup failing to open at all.
`script-src` and `frame-src` both need `https://www.google.com`; `connect-src`
is already covered by `https://*.googleapis.com`.

The reason it reached production is worth keeping: `startAppCheck` wraps only
`initializeAppCheck` in try/catch, and the script load happens asynchronously
inside the provider afterwards, so a blocked script throws nowhere anything is
watching. There is no error state -- just a slow page. Any future change to how
App Check is loaded needs checking against the live response headers, not the
build.

**Domain gap to settle before enforcement.** The reCAPTCHA key covers the apex
and `www` forms of `alistragis.com`, `.co.uk` and `.uk`. Production also
answers on `fibre-gis-v2.vercel.app` and the long `alistragis-…vercel.app`
alias, which are not registered. Unverified today and harmless; a lockout the
moment enforcement is on.

### Per-user rate limiting — shipped 2026-08-21, live

Twelve operations capped per user, per operation. Policy in
`functions/src/api/rateLimitPolicy.ts`, enforcement in
`functions/src/api/rateLimit.ts`, full detail in `docs/RATE_LIMITING.md`.

| Operation group | Limit |
| --- | --- |
| Map saves, deletes, joint mapping saves | 120/min |
| Branding uploads | 20/min |
| Bulk upserts, FAS/SB import, map audit, Excel export | 10/min |
| Licence administration | 30/min |
| `createCompany` | 5 per 5 min |
| `backupAndDeleteCompany` | 2 per 10 min |

**Not all 147 callables, by choice.** The Firestore counter costs a read and a
write per call, so putting it on every read path would add a guaranteed write
to operations that only read — spending money to save money. It goes where the
operation's own cost is high enough that the counter disappears against it, or
where abuse is expensive.

The `fridayRateLimits` limiter described above, and the licence limiter that
was the only one in the product code, are the ancestors of this. The licence
one is folded into the shared implementation at its original 30/min, so its
behaviour is unchanged and there is now one implementation rather than two.

**Security fix found while building it.** `backendRateLimits` is a root-level
collection, and the root catch-all in `firestore.rules` granted read and write
to any root-privileged user — so a super admin's browser could have cleared its
own counter, and root-privileged users are precisely the ones who can call the
expensive operations. Fixed by excluding it in the catch-all itself, not by
adding a narrower `allow ...: if false`, which would not have worked: Firestore
rules are OR-ed across every matching path, so a more specific deny never
overrides a broader allow. Two regression tests in
`tests/firestore-rules.rules-test.mjs` cover it (30 rules tests passing).

**Firestore TTL policy enabled** on `backendRateLimits.expiresAt`, state
`ACTIVE`, so counters delete themselves rather than accumulating. Worth noting
this is the project's *only* TTL policy and the only automated data cleanup of
any kind — see the retention gap in [[Data Retention Schedule]].

### Still open from the original list

- **Usage/budget alerts** in the GCP console: still unverified from code.
- **Read-cost scaling** as data grows: unchanged, still a product concern.
- **No per-company or per-IP limit.** Everything is per user, so ten users in
  one company can do ten times the traffic. Acceptable while seats are licensed
  and accounts are administrator-created.

## Not addressed at the time of the 2026-08-08 review

- **Firebase App Check**: not configured anywhere in the codebase. App Check verifies that requests to Cloud Functions/Firestore/Storage come from genuine app instances (via reCAPTCHA or similar), which is the standard modern mechanism for stopping scripted abuse that already has a valid account/token — CORS restriction (`callableCors`) only stops casual browser-based cross-origin calls, not a script or `curl` request with a valid ID token, since CORS is purely browser-enforced. This is the single most impactful thing left to do for this stage, but implementing it properly means client SDK integration plus `enforceAppCheck: true` across every function, and misconfiguring it risks blocking real users — flagging as the top recommendation rather than rushing it in this pass.
- **Usage/budget alerts**: Google Cloud Billing budget alerts are configured in the GCP Console, not in this repo — could not verify their existence or thresholds from code. Worth confirming directly in the console.
- **Read-cost scaling as data grows**: several list endpoints (`listCompanyEmployees`, `loadAllTickets`, etc.) do unbounded `.get()` calls with no pagination. Not an abuse vector today (they're authenticated, role-gated, and tenant-scoped), but as any one company's data grows into the thousands of records, "load all X" becomes a genuinely expensive read repeated on every page load. A product/scaling concern for later, not a security gap.
