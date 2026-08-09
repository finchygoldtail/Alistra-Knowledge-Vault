---
status: live
updated: 2026-08-08
related: ["[[Permissions Model]]", "[[Role Matrix]]", "[[Decision Log]]", "[[Vercel Deployment]]", "[[Security Overview]]"]
---

# Current State Validation

> **CORRECTION (2026-08-08, later same day):** Everything below this notice was
> validated against `C:\Projects\AlistraGIS`, which turned out to be the
> **wrong repository** for commercial-readiness purposes. AlistraGIS's own
> `START_HERE.md` states it is a fresh rewrite that explicitly has
> not started migrating Map/Assets/Firestore persistence yet, and names
> `C:\Projects\fibre-gis` as "the live latest GitHub checkout." fibre-gis is
> confirmed live by its own README (Vercel serves `alistragis.com` /
> `www.alistragis.uk` directly from it) and its commit history (the Round 2–4
> audits the vault already documents happened in this repo).
>
> Everything below remains an accurate record of AlistraGIS's state and is
> still useful if/when that rewrite resumes, but **it does not describe the
> live product**. The equivalent, corrected findings for fibre-gis are in
> [[Decision Log]] (2026-08-08 entries) — in short: a real, live P0 was found
> and fixed there (a role gate on `mapAssets`/`mapAssetBackups` that looked
> correct but was silently overridden by a generic catch-all rule, confirmed
> via a passing/failing emulator test before and after the fix), plus an
> audit-log field-forgery gap in `createAssetChangeLog`. Both are fixed,
> verified (7/7 new rules tests, clean typecheck/build, 267/267 existing
> tests), and **deployed to production** the same day (`firestore:rules` and
> `functions:createAssetChangeLog`, both confirmed successful).
>
> Going forward, treat `fibre-gis` as the default target for this programme
> unless a task explicitly says AlistraGIS.

Per Development Rule 1 of the Commercial Go-Live programme: this is a factual comparison of what the vault documents against what `C:\Projects\AlistraGIS` actually does, produced **before** any architectural or security changes. No fixes have been made yet — this is the "understand before changing" checkpoint.

Sources: direct code inspection of `AlistraGIS` (firestore.rules, storage.rules, Cloud Functions in `backend/src`, frontend write paths in `map-frontend/src`) cross-referenced against the vault's `02 Architecture`, `09 Security and Permissions`, `10 Deployment and Infrastructure`, `00 Dashboard/Decision Log.md`, `08 Testing and Bugs/Active Bugs.md`, and `07 Codex Tasks/Completed Tasks.md`.

Priority tags follow the programme's P0–P3 scale (P0 = commercial blocker).

---

## 1. Map asset edit/delete enforcement — **P0, confirmed and worse than documented**

**Documented state:** `[[Decision Log]]` (2026-08-04 entry, linked from `[[Permissions Model]]`, status "needs decision") already identifies that map assets are stored as shared per-business chunk documents (`mapAssets/main/chunks/*`), that Firestore rules "can't distinguish 'add an asset' from 'delete one' within the same chunk write," and that the real fix needs either a data model change or a Cloud Function write gateway "as already used for `assetChangeLogs`." This framing implies the gap is a known, scoped, rules-engine limitation with a CF-gateway precedent to follow.

**Actual code state:**
- `map-frontend/firestore.rules` has **no** collection-specific rule for `mapAssets/**`, `mapAssetBackups/**`, or `assetChangeLogs/**`. They fall through the generic catch-all (`isKnownBusinessUser(businessId)`), which checks only active business membership — **no role check at all**, for any role including `"user"`.
- A genuinely role-checked write path *does* exist: Cloud Function callables in `backend/src/storage/storageCallables.ts` (`saveCompanyMapAssets`, `upsertCompanyMapAsset`, `deleteCompanyMapAsset`, etc.) explicitly reject role `"user"` server-side.
- However, the primary frontend save path (`map-frontend/src/services/mapAssetStorage.ts:saveMapAssetsToFirestore`, wired through `mapSaveCoordinator.ts`) writes **directly to Firestore** via `setDoc`/`deleteDoc`, bypassing the role-checked callables entirely.
- Which path runs is decided by `map-frontend/src/storage/services/storageFeatureFlags.ts`, which checks a **browser `localStorage` key** (`alistra-use-backend-storage-api`) before falling back to a build-time env var. Any signed-in user can set this key from devtools and force the app onto the unchecked direct-Firestore path.
- The `assetChangeLogs` CF gateway cited in the Decision Log as the precedent (`createAssetChangeLog`, via `assertCompanyMember`) checks business membership only, **not role** — so it is not actually an example of role-based enforcement, only of membership-based enforcement.

**Difference:** The vault treats this as "no clean fix yet, decision pending, but a CF-gateway pattern already exists to model the fix on." The actual situation is: a CF-gateway path exists and does check role, but it is **routed around by a client-controlled toggle**, and the cited precedent (`assetChangeLogs`) does not itself enforce role. The severity is understated — this isn't just "no server-side fix yet," it's "a server-side fix exists but has a live, trivially-flippable bypass," which is a more urgent framing for a P0 register.

**Required correction:** Update `[[Decision Log]]` to reflect the bypass mechanism precisely (not just the rules limitation), and treat this as the Stage 2 P0 RBAC item per the go-live plan — remove the client-controlled fallback, make the CF-gateway path the only path (or add matching role checks at the Firestore rules layer as a backstop), and add role checks to the `assetChangeLogs` CF gateway itself since audit-log integrity depends on it.

---

## 2. Audit log (`assetChangeLogs`) integrity — **P0, new finding not in vault**

**Documented state:** Not separately called out anywhere in the vault as its own risk; only referenced in passing as the CF-gateway precedent (see §1). `R&D/R&D Risk Register.md` (RND-R15, "Audit logs can be forged, altered, deleted or duplicated") flags this as a *risk register* entry in the R&D/tax-claim tracker, not in the product security docs, and without the specific mechanism.

**Actual code state:** Two problems compound: (a) `assetChangeLogs/*` has no Firestore-rules-level protection beyond business membership — any active member, any role, can write/delete audit-log documents directly via the client SDK; (b) the CF callable path (`createAssetChangeLog`) checks membership only, not role, so even the "safe" path doesn't restrict who can create entries. The repo's own scanner previously flagged an even earlier version of this code doing raw `addDoc` writes with no callable at all (`friday-health.md`, finding FRI-048, severity "high").

**Difference:** RND-R15 correctly predicts the risk category but the vault has no confirmed, code-verified finding tying it to `assetChangeLogs` specifically, and doesn't distinguish it from the general map-asset gap.

**Required correction:** Treat as its own P0 line in `02 Security Hardening Register.md` once created (Stage 1 of the commercial-readiness folder) — audit logs must become server-write-only (Firestore rule: `write: if false` for clients, all writes via an Admin-SDK Cloud Function with role/immutability checks) since they are the evidence trail the rest of the security programme relies on.

---

## 3. Project-level membership / scoping — **P1, confirmed gap, partially documented as aspiration**

**Documented state:** `[[Multi-Tenant Architecture]]` states, as a requirement rather than a description: "Project-level access for map, production, audit and reporting data" should exist, and "tenant-aware API enforcement" should apply. This reads as an intended design, not a confirmed implementation.

**Actual code state:** No project-membership document, collection, or ACL exists anywhere in Firestore rules or Cloud Functions (`grep -rl "projectMembers|ProjectMembership"` returns nothing). `projectId`/`areaId` are free-form fields on assets, not access-control boundaries. Any active member of a business can read/write any project's assets within that business. This matches the *separate, already-accepted* gap recorded in `[[Active Bugs]]` (2026-08-07): "Any business member can read (not write) any other member's assets/photos/employees/etc. — accepted architectural gap since 2026-08-04." Note that entry describes a **read**-only gap as accepted; the code shows the same absence of project scoping also applies to **write** access for map assets and storage uploads, which has not been separately accepted.

**Difference:** The vault's read-only "accepted gap" framing does not cover the write-side exposure the code shows (business members can write into any project, not just read). This wasn't consciously accepted and should be.

**Required correction:** Either explicitly extend the accepted-risk note to cover writes (if that's a deliberate v1 scope decision) or add project-scoped write checks. This should be evaluated as part of Stage 2/3 (RBAC fix + tenant isolation) rather than left as an implicit extension of a read-only exception.

---

## 4. Custom claims for "Build Partners" — **P2, documentation describes a mechanism that doesn't exist in code**

**Documented state:** `[[Role Matrix]]` states Build Partners are "a separate identity axis... resolved via a Firebase custom claim."

**Actual code state:** No use of Firebase custom claims exists anywhere in the codebase — `setCustomUserClaims`/`customClaims` returns zero matches in `backend/src` or `map-frontend/src`. All role/membership data is read from Firestore documents client-side, not from auth token claims.

**Difference:** Either the Build Partners feature hasn't been built yet and the doc is describing a plan, or an earlier implementation was removed. Either way, the documented mechanism does not currently exist.

**Required correction:** Confirm with the team whether Build Partners is implemented elsewhere/pending, and either mark `[[Role Matrix]]` as documenting a planned-not-built feature, or scope the actual implementation. Low urgency relative to P0/P1 items above, but worth resolving before it's assumed to be a working control.

---

## 5. Platform-owner bootstrap (`OWNER_EMAILS`) — **P1, undocumented, duplicated in 5 places**

**Documented state:** Not mentioned anywhere in the vault.

**Actual code state:** A hardcoded owner email (`alistairlgrantham@gmail.com`) grants implicit `super_admin`, independently evaluated in five separate places: `backend/src/index.ts`, `backend/src/storage/storageAccess.ts`, `map-frontend/firestore.rules`, `map-frontend/storage.rules`, and `map-frontend/src/context/UserRoleContext.tsx`.

**Difference:** This is a real, working privileged-access mechanism with no documentation and no single source of truth — a change to one location without the others would create an inconsistency (e.g. a hosting-rules bypass that Cloud Functions don't recognize, or vice versa).

**Required correction:** Document this bootstrap mechanism explicitly (likely in `[[Authentication]]` or a new secrets/credential note), and consider consolidating to a single constant or Firestore-driven "platform owners" list read by all five checks, so ownership changes don't require five coordinated edits.

---

## 6. Authentication implementation — **P2, documentation understates what's built (safe direction, but inaccurate)**

**Documented state:** `[[Authentication]]` is a one-line stub: "AlistraGIS uses Firebase Authentication with Google and email authentication," with MFA and password reset not described (MFA is only mentioned incidentally in `[[Concurrent Login Control]]`).

**Actual code state:** `map-frontend/src/components/AuthGate.tsx` implements a substantially more complete flow: email/password and Google sign-in, password reset (`sendPasswordResetEmail`), mandatory email verification gating, TOTP MFA enrollment and sign-in challenge resolution, and a forced-password-change flow enforced via a Cloud Function (`changeOwnPassword`, 8+ char minimum server-side).

**Difference:** Documentation lags well behind implementation here — not a security risk, but means anyone relying on the vault to understand the auth surface (e.g. for the GDPR data map or a pen-test scope in later stages) would miss MFA enrollment, forced password change, and email verification entirely.

**Required correction:** Expand `[[Authentication]]` to describe the actual flow (this vault gap is low-risk but directly feeds Stage 8 "Authentication Hardening" and Stage 13 "GDPR Data Map" — both need an accurate picture of what auth data/flows exist).

---

## 7. Deployment configuration — **P2, confusing but functional dual Firebase config**

**Documented state:** `[[Vercel Deployment]]` (the vault's most detailed and accurate deployment doc) correctly states Vercel is the only thing serving `alistragis.com`/`www.alistragis.uk`, deploys automatically on push to `main`, and that `firebase deploy` is "only ever needed for `--only functions` or `--only firestore:rules`." This matches [[fibre-gis-deployment-model]] guidance already held elsewhere: frontend ships via `git push origin main` → Vercel, not `firebase deploy --only hosting`.

**Actual code state:** There are **two separate `firebase.json` files** with different, overlapping scopes:
- Repo-root `firebase.json`: hosting site `"alistragis"` (serves only a static stub/health page, not the real app), functions source `backend/` — **no `firestore` or `storage` key at all**.
- `map-frontend/firebase.json`: hosting site `"fibre-gis-v2"` (301-redirects everything to `alistragis.com`), **does** declare `firestore.rules: "firestore.rules"` and `storage.rules: "storage.rules"` (correctly pointing at the real rules files in that directory), and a `functions` source pointing at `map-frontend/functions/` — **which does not exist on disk**.

So: `firebase deploy --only firestore:rules` only works correctly if run from inside `map-frontend/` (using its `.firebaserc` → `fibre-gis-v2`); run from the repo root it would silently no-op (root config has no firestore key). `firebase deploy --only functions` from `map-frontend/` would fail (missing functions dir); the real functions deploy is `backend`'s script (`firebase deploy --only functions`, from repo root).

**Difference:** The vault's deployment guidance is directionally correct but doesn't capture that there are two independent Firebase configs whose commands only work from specific directories, with one dead/misconfigured reference (`map-frontend/functions`). This is exactly the kind of ambiguity that leads to a rules change being drafted correctly but deployed from the wrong directory and silently not applying.

**Required correction:** Document the dual-config split explicitly in `[[Vercel Deployment]]` or a new deployment note: rules/storage deploys must run from `map-frontend/`, functions deploys must run from repo root targeting `backend/`, and the stale `map-frontend/firebase.json` functions reference should be removed or fixed. This directly affects Stage 4/5 (Firestore/Storage rules work) in the go-live plan — any rules fix must be deployed and verified from the correct directory, and that verification step should be explicit in whatever process replaces STAGE 4/5.

---

## 8. Testing plan coverage — **P1, no documented security/permission test methodology**

**Documented state:** `[[Regression Testing]]` lists "Permissions" as an area to cover but with no specific test cases or methodology. No document describes a Firestore-rules emulator test suite, a role-matrix test plan, or tenant-isolation test cases.

**Actual code state:** `07 Codex Tasks/Completed Tasks.md` mentions Firestore rules tests exist in the codebase but are "blocked by the same missing-Java-for-the-emulator constraint" — i.e. a rules test suite exists in principle but cannot currently run.

**Difference:** The vault's testing docs don't reflect that rules tests exist-but-are-blocked; this is operationally important context missing from the testing plan.

**Required correction:** Fix the Java/emulator blocker before Stage 4 (Firestore rules work) — the plan explicitly requires "No security-rule deployment without passing tests," which is currently not achievable. Record this blocker and its resolution in the testing plan.

---

## Summary table

| # | Area | Priority | Status |
|---|------|----------|--------|
| 1 | Map asset edit/delete enforcement | **P0** | Confirmed, more severe than documented — feeds Stage 2 |
| 2 | `assetChangeLogs` audit integrity | **P0** | New finding, not previously isolated in vault |
| 3 | Project-level write scoping | P1 | Confirmed gap; write-side not covered by existing accepted-risk note |
| 4 | `OWNER_EMAILS` bootstrap | P1 | Undocumented, duplicated in 5 locations |
| 5 | Firestore rules test suite blocked | P1 | Emulator tests exist but can't run (Java dependency) |
| 6 | Dual Firebase config / deploy paths | P2 | Functional but confusing; one dead functions reference |
| 7 | Authentication doc completeness | P2 | Docs understate real (safe) implementation |
| 8 | Build Partners custom claims | P2 | Documented mechanism not present in code |

**No architectural or security changes have been made as part of this document.** Items 1 and 2 are the P0 blockers that gate Stage 2 (server-side RBAC fix) of the commercial go-live plan and should be scoped next.
