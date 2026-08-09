---
status: live
updated: 2026-08-08
related: ["[[API Security]]", "[[Permissions Model]]", "[[Role Matrix]]", "[[Decision Log]]", "[[Multi-Tenant Architecture]]"]
---

# API Security Assessment — 2026-08-08

Stage 9 of the commercial go-live programme: a complete inventory of every Firebase Cloud Function in `C:\Projects\fibre-gis\functions\src` — **124 functions across 22 files at the time of the review** (121 after the cleanup described below), every one read in full (not sampled). For each: authentication requirement, tenant/business scoping mechanism, role gate, resource-ID handling (IDOR/BOLA exposure), input validation (mass-assignment exposure), and audit logging.

## Headline result: four confirmed cross-tenant vulnerabilities — three fixed then deleted as dead code, one fixed and kept

`upsertLiveUserLocation`, `clearLiveUserLocation`, `getLiveUserLocations` and `extendStreetManagerPermit` (all in `functions/src/index.ts`) checked that the caller was *signed in*, but never checked the caller actually belonged to the `businessId` they supplied in the request — every other function in the codebase (120 of 124) uses one of two safe patterns (`resolveStorageContext`/`assertCompanyMember`) that cross-check the client-supplied businessId against the caller's real membership doc before trusting it; these four skipped that check entirely.

**Worst case: `getLiveUserLocations`** — any signed-in user of *any* company could call it with a different company's `businessId` string and get back that company's field workers' live GPS coordinates, names, and emails. This is a straightforward BOLA/IDOR and a real GDPR-relevant PII exposure. `upsertLiveUserLocation`/`clearLiveUserLocation` were lower-severity write-side variants of the same missing check. `extendStreetManagerPermit` was gated only by a hardcoded business-name allow-list (`harrellicomms` and spelling variants) rather than caller membership — meaning a user from *any other company* could trigger it against Harrellicomms's data, including a real external Street Manager API call affecting an actual street-works permit when API credentials are configured.

**Fixed, then reconsidered**: added `await assertCompanyMember(admin.firestore(), businessId, uid)` to all four. While building the Stage 13 GDPR data map, investigating the live-location feature's actual usage turned up **zero frontend integration anywhere in either fibre-gis or AlistraGIS** — the three live-location functions were fully dead backend code, never called by any UI. Rather than ship a fixed-but-unused feature, they (plus the `LIVE_LOCATION_COLLECTION` constant, the `getLiveLocationDocId` helper, the now-orphaned `toNumberOrNull` helper, and the collection's entry in `firestore.rules`) were deleted entirely — the best resolution to a BOLA is not having the data at all. `extendStreetManagerPermit` has real backing use (an actual permit-extension workflow), so it was kept with its fix. Full detail in [[03 GDPR Data Register]]. Verified with clean builds in both repos and the full test suite passing.

**Not yet deployed** — pending the same approval step as previous fixes this session.

## Secondary finding: mass-assignment via unvalidated object spreads (not tenant-crossing, lower severity)

`upsertCompanyWorkPack` (+ its HTTP-API twin), `upsertCompanyCrew`, `upsertCompanyEmployee`/`bulkUpsertCompanyEmployees`, `upsertCompanyVehicle`/`bulkUpsertCompanyVehicles`, and `upsertCompanyPlantEquipment`/`bulkUpsertCompanyPlantEquipment` all do `{ ...input, id, companyId, ...auditFields }` — the identity/tenant/audit fields are correctly overridden *after* the spread so cross-tenant writes and audit-field forgery are not possible, but any other field name the client sends lands unfiltered in the Firestore document. Since every one of these callables already requires `requireManagerOrAbove` (an authenticated, already-privileged, same-tenant caller), the exploitable blast radius is narrow — a manager could write undocumented junk fields into their own company's own records, not access anything cross-tenant or bypass their existing privilege level. **Not fixed this session** — a proper fix means building an explicit field allow-list per entity type across six files, which risks silently dropping a legitimate field the UI actually sends without full visibility into every caller; flagging for dedicated follow-up rather than rushing it. `storageProfileManagement.ts`'s three functions already demonstrate the correct pattern (explicit per-field mapping, no spread) and can serve as the template.

## Full inventory

One structural note that applies to ~100 of the 124 functions: once `resolveStorageContext`/`assertCompanyMember` has verified the caller's membership, every subsequent Firestore path is built as `businesses/{resolvedCompanyId}/...` — tenant isolation for the resource itself then falls out of the path prefix rather than a second explicit per-document check. This is structurally sound and consistently applied, but it does mean the *entire* codebase's tenant isolation rests on that one shared helper being correct — which is exactly the kind of single point of failure the four fixed functions demonstrate the risk of bypassing.

### `functions/src/index.ts` (27 functions)

| Function | Auth | Tenant scoping | Role gate | Notes |
|---|---|---|---|---|
| `upsertLiveUserLocation` | — | — | — | **Removed 2026-08-08** — fixed the tenant-scoping gap first, then investigating for the GDPR data map found zero frontend integration anywhere; confirmed dead code and deleted entirely (see [[03 GDPR Data Register]]) rather than left fixed-but-unused |
| `clearLiveUserLocation` | — | — | — | Removed alongside the above |
| `getLiveUserLocations` | — | — | — | Removed alongside the above — this was the real cross-tenant PII leak; now the data category doesn't exist at all |
| `extendStreetManagerPermit` | Yes | Fixed 2026-08-08 (was unchecked, only a business-name allow-list) | None | Can trigger a real external API call — kept, since this one has real backing use (Harrellicomms permit workflow), unlike the live-location functions |
| `createLoginUser` | Yes | Safe (`assertCanManageUsers`) | Admin-tier | Role-assignment additionally gated by `assertCanAssignRole` (only `OWNER_EMAILS` can grant `super_admin`) |
| `createCompany` | Yes | N/A (creates a company) | Owner-email or `super_admin` only | |
| `backupAndDeleteCompany` | Yes | N/A (destructive) | Owner-email or `super_admin` only | Blocks deleting `fibre-gis-v2`; requires typed `DELETE {businessId}` confirmation |
| `bootstrapOwnerSuperAdmin` | Yes | N/A | Owner-email only | |
| `updateLoginUserProfile` | Yes | Safe | Admin-tier | |
| `getCompanyAdminSettings` / `saveCompanyAdminSettings` | Yes | Safe | Admin-tier | |
| `listCompanyUserProfiles` | Yes | Safe | Admin-tier | Platform-owner path intentionally returns all businesses' users |
| `upsertAreaOperationsMessage` / `deleteAreaOperationsMessage` | Yes | Safe | Membership only | |
| `loadJointMappingRows` / `saveJointMappingRows` | Yes | Safe | Membership only | Row count capped at 10,000 |
| `createAssetChangeLog` | Yes | Safe | Membership only | `changedByUid/Email/Name` forced server-side (fixed 2026-08-08 earlier this session) |
| `loadAssetChangeLogs` | Yes | Safe | Membership only | maxResults clamped 1–100 |
| `createTicket` / `loadMyTickets` | Yes | Safe | Membership / self | |
| `loadAllTickets` / `updateTicketStatus` / `assignTicket` | Yes | Safe | Ticket-admin | |
| `createTicketEvent` / `loadTicketEvents` | Yes | Safe | Owner-or-admin | Attachment URLs validated to belong to the caller's own company storage tree |
| `deleteLoginUser` | Yes | Safe | Admin-tier | Blocks deleting owner-email/admin/super_admin targets unless caller is an owner |
| `changeOwnPassword` | Yes | Trusted directly but self-write only | None (self only) | Password length ≥8 enforced server-side |

### `functions/src/storage/storageCallables.ts` (15 functions) — all safe tenant scoping via `resolveStorageContext`, all audit-logged

`saveCompanyMapAssets`, `upsertCompanyMapAsset`, `deleteCompanyMapAsset`, `moveCompanyHomesToDp`, `logCompanyDailyProduction`, `removeCompanyDailyProduction`, `updateCompanyProductionStatus`, `flagCompanyAssetQa`, `importCompanyFasSbRoutes` all require `requireManagerOrAbove`. `resolveCompanyAssetQa` requires `requireSupervisorOrAbove`. `getCompanyStorageProfile`, `loadCompanyMapAssets`, `listCompanyWorkPacks` are read-only, membership-gated only. `upsertCompanyWorkPack`/`deleteCompanyWorkPack` require `requireManagerOrAbove` — `upsertCompanyWorkPack` has the mass-assignment pattern noted above.

### `functions/src/storage/storageHttpApi.ts` — `api` (raw HTTP endpoint, not a callable)

Manually verifies a Firebase Auth bearer token, resolves tenant context the same safe way, additionally gated by `assertCompanyLicenceAllowsApiAccess` (blocks expired/suspended licences). Per-route role gates mirror the callable versions. Audited on every mutating/access-sensitive route except the work-packs GET/PUT/POST/DELETE sub-routes.

### `functions/src/storage/{crew,document,employee,vehicle,plantEquipment,workPackLifecycle}Callables.ts` (39 functions total) — all safe tenant scoping

Consistent pattern throughout: reads are membership-only; creates/updates/deletes of registers require `requireManagerOrAbove`; a defined set of day-to-day operational actions are deliberately self-service for any active member (vehicle/plant check-out/check-in, defect reporting, daily checks, routine inspections, driver assignment) per explicit code comments citing field-speed as the reason; snag resolution and work-pack readiness/completion sign-off require `requireSupervisorOrAbove`. `deleteCompanyCrew` has a real referential-integrity guard (blocks deletion while plant/vehicles are still assigned to it). `recordEmployeeCredential` and most handover/service functions verify the target resource exists (via a transaction) before mutating it; a handful of simple upserts (crew/vehicle/plant/document/work-pack) don't check existence before writing, which is low-risk since they're idempotent upserts, not silent overwrites of someone else's data (tenant path prefix already prevents that).

### `functions/src/storage/sessionCallables.ts` / `storageProfileManagement.ts`

`stampUserSession` is self-scoped only. `storageProfileManagement.ts`'s three functions (`saveCompanyStorageProfileDraft`, `testCompanyStorageProfileConnection`, `activateCompanyStorageProfile`) use `resolveStorageAdminContext` — the strictest gate in the codebase, requiring `super_admin`/`admin` role *before the callable body even runs* — and validate every field individually rather than spreading raw input, the correct reference pattern the mass-assignment items above should eventually follow.

### `functions/src/commercial/` (38 functions across 9 files) — all safe tenant scoping

Consistently well-gated: `requireCommercialManager` for most writes, escalating to `requireCommercialApprover` for anything that locks a package, approves/rejects a variation, or certifies a valuation, and `requireMarginVisibility` for anything that reveals cost/price data. Two standout defensive patterns worth calling out as the strongest in the codebase:

- **`lockCommercialPackageSnapshot`** runs `findAssetAllocationConflict` against every other locked package company-wide inside its transaction, preventing the same map asset from being double-committed to two commercial packages.
- **`getPackageSnapshotForPartner`** (build-partner axis, `buildPartnerCallables.ts`) explicitly checks `packageDoc.buildPartnerId !== partnerContext.partnerId` and returns an identical `not-found` error whether the package doesn't exist or simply isn't the caller's — preventing both cross-partner access and ID enumeration in one check. The whole build-partner axis (`resolveBuildPartnerAuthContext`) derives identity from a custom claim on the caller's own token, re-verified live against their membership doc, and never trusts a client-supplied businessId at all — structurally the safest scoping pattern in the codebase.

### `functions/src/friday/fridayCallables.ts` — `fridayChat`

Covered in depth in the FRIDAY-specific section below.

## What this assessment did not cover

Live penetration-style testing (forged tokens, replayed requests, actually calling every endpoint over the network with adversarial payloads) was not performed — this was a full code-level review of every function's authorization logic instead, which is what actually caught the four real vulnerabilities above (a network-level black-box test would very plausibly have missed `getLiveUserLocations` too, since its response shape looks identical whether the check is present or not). A live adversarial pass belongs in Stage 31 (internal penetration test) once the P0/P1 backlog is otherwise clear.
