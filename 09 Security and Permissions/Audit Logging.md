---
title: Audit Logging
type: security
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-08
tags: [security, audit]
---

# Audit Logging

Audit logging records sensitive actions for support, security and accountability.

## Events

- Authentication and session events from [[Authentication]].
- Permission changes from [[Manage Users]].
- Data changes through [[API Catalogue]].

## Actual implemented model (Stage 12 review, 2026-08-08)

`businesses/{companyId}/auditEvents` is the unified audit trail — server-write-only since the Stage 4 rules fix ([[Decision Log]]), written via `writeStorageAuditEvent()`, recording `actingUserId`, `actingRole`, `eventType`, `success`/`safeErrorCode`, `timestamp` (server-stamped), and now an optional `details` map for target-resource context (e.g. which user got created/deleted, what role was assigned). `assetChangeLogs` is a second, purpose-built trail specifically for map asset edits, also server-write-only, with its identity fields (`changedByUid/Email/Name`) forced from the verified caller's Auth record rather than trusted from the client (fixed the same day as the Stage 4 rules work).

Cross-checked coverage against this stage's required event list:

| Required event | Status |
|---|---|
| User creation | **Was missing, fixed today** — `createLoginUser` now logs `admin.user.created` |
| User deletion | **Was missing, fixed today** — `deleteLoginUser` now logs `admin.user.deleted` |
| Role change / permission changes | **Was missing, fixed today** — `updateLoginUserProfile` now logs `admin.user.updated` with the target uid/role |
| Organisation changes | **Was missing, fixed today** — `createCompany` now logs `admin.company.created` |
| Configuration changes | **Was missing, fixed today** — `saveCompanyAdminSettings` now logs `admin.settings.updated` |
| Data export | Partially covered — `exportCommercialPackageExcel` is logged; other exports (CSV/Excel report generation) appear to happen entirely client-side with no server round-trip, so there's no server-side record of who exported what for those flows. Not fixed this session — would need moving those export flows server-side first, which is a bigger architectural change than adding a log call. |
| Sensitive API actions | Well covered across storage/commercial callables (see [[API Security Assessment 2026-08-08]]) — the gap was specifically the user/org-management cluster in `index.ts`, now closed |
| Admin login | **Not implemented.** Would need a Firebase Auth trigger (blocking function or `onCreate`-style hook) to capture sign-in events into the app's own audit trail — Firebase Auth's own console activity log is a partial substitute today but isn't tenant-aware or queryable alongside the rest of `auditEvents`. Flagged, not built this session. |
| Project deletion | Not applicable to the current data model — projects aren't a top-level deletable entity (no dedicated delete-project function exists); revisit if that changes. |
| Security incidents | No dedicated detection/aggregation mechanism (e.g. alerting on a spike of `storage.access.denied`/`commercial.access.denied` events). This is SIEM-adjacent territory the original plan already treats as a P3/future-enterprise capability, not a v1 blocker. |

Before today, the gap was backwards from what you'd want: the highest-privilege actions (who can create/delete users, change roles, change company-wide settings) were the *least* observable, while routine day-to-day storage/commercial actions were already well logged. That asymmetry is now closed for the five events above. Verified with a clean build and the existing 267-test suite passing; **not yet deployed**.

