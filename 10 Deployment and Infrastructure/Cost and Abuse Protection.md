---
status: live
updated: 2026-08-08
related: ["[[Decision Log]]", "[[FRIDAY Security Model]]", "[[API Security Assessment 2026-08-08]]"]
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

## Not addressed this session

- **Firebase App Check**: not configured anywhere in the codebase. App Check verifies that requests to Cloud Functions/Firestore/Storage come from genuine app instances (via reCAPTCHA or similar), which is the standard modern mechanism for stopping scripted abuse that already has a valid account/token — CORS restriction (`callableCors`) only stops casual browser-based cross-origin calls, not a script or `curl` request with a valid ID token, since CORS is purely browser-enforced. This is the single most impactful thing left to do for this stage, but implementing it properly means client SDK integration plus `enforceAppCheck: true` across every function, and misconfiguring it risks blocking real users — flagging as the top recommendation rather than rushing it in this pass.
- **Usage/budget alerts**: Google Cloud Billing budget alerts are configured in the GCP Console, not in this repo — could not verify their existence or thresholds from code. Worth confirming directly in the console.
- **Read-cost scaling as data grows**: several list endpoints (`listCompanyEmployees`, `loadAllTickets`, etc.) do unbounded `.get()` calls with no pagination. Not an abuse vector today (they're authenticated, role-gated, and tenant-scoped), but as any one company's data grows into the thousands of records, "load all X" becomes a genuinely expensive read repeated on every page load. A product/scaling concern for later, not a security gap.
