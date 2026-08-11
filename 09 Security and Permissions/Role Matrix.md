---
title: Role Matrix
type: security
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-11
tags: [security, roles]
---

# Role Matrix

| Role | Draw | Navigate | Measure | Toggle Layers | Manage Users |
| --- | --- | --- | --- | --- | --- |
| Super-admin | Yes | Yes | Yes | Yes | Yes |
| Admin | Yes | Yes | Yes | Yes | Yes, scoped |
| Manager | No | Yes | Yes | Yes | No |
| Supervisor | No | Yes | Yes | Yes | No |
| User | No | Yes | Yes | Yes | No |

## Tenant boundary clarification (2026-08-11)

Tenant administrators receive user-management authority only from an explicitly active membership in the requested business. A root `users/{uid}` profile carrying `admin` no longer grants cross-tenant authority. Cross-tenant platform access is limited to the hardcoded platform owner or an explicitly active root `super_admin`; inactive and missing-`active` profiles fail closed.

## Supervisor (added 2026-08-07)

Sits between Manager and User. Same map permissions as Manager/User (no drawing), but with additional server-side write access Manager and above already had and User never had:

- Approve work-pack readiness, sign off crew-reported completion.
- Resolve QA flags and work-pack snags.
- View all crews' data.

Deliberately **excluded** from Supervisor (stays Manager+): plant/vehicle/employee register edits and deletes, cost/service/calibration data, map-asset edits, work-pack CRUD, company-wide settings. Enforced server-side by two distinct callable-side helpers rather than one parameterised one — `requireManagerOrAbove` (excludes both User and Supervisor) and `requireSupervisorOrAbove` (excludes only User) — see [[Decision Log]].

## Commercial gates (added 2026-08-07)

[[Commercial Subcontracting]] follows the same separate-non-parameterised-helper convention, in its own file (`commercialRoleGates.ts`, not merged into the main `roleGates.ts`):

- `requireCommercialManager` — excludes User, Supervisor. Package/recipe/rate-card creation and editing.
- `requireCommercialApprover` — excludes User, Supervisor, **and Manager**. Package locking, variation approval, valuation certification.
- `requireMarginVisibility` — excludes User, Supervisor. Read-only gate for cost/rate/margin data, independent of the write gates above.

**Build Partners are not a role tier at all** — a separate identity axis (external subcontractor login, single-business scoped) resolved via a Firebase custom claim, never through `roleGates.ts` or the roles table above. See [[Commercial API]].

See [[Permissions Model]], [[Manage Users]] and [[Concurrent Login Control]].
