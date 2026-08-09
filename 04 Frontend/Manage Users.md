---
title: Manage Users
type: frontend
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [frontend, users, permissions]
---

# Manage Users

Manage Users supports company and project user administration.

## Requirements

- Assign user roles from [[Role Matrix]], including the Supervisor tier added 2026-08-07.
- Scope access through [[Multi-Tenant Architecture]].
- Make drawing restrictions clear from [[Permissions Model]].

## Client Modules and Employees (2026-08-07)

- Crews is toggleable in the Client Modules admin screen (`clientFeatures.ts`'s `CLIENT_FEATURE_OPTIONS`) as a standalone Core toggle rather than a full Project Workspace tab — it stays reachable only via Admin Utilities.
- Plant Equipment, Vehicles and Employees were briefly an admin-panel section here, then moved same-day into the Project Workspace's Management tab group — see below.

## Plant Equipment, Vehicles and Employees moved into the Management tab group (2026-08-07)

Requested same day as the initial build. Plant Equipment and Vehicles were Project Workspace tabs under the "Field" group; Employees (roster, credentials, Excel bulk import) was a Manage Users admin-panel section. All three are now full Project Workspace tabs filed under the "Management" tab group (`workspaceTabGroups` in `projectWorkspaceConfig.tsx`), alongside the existing Management/Commercial/BOQ/Admin Utilities tabs — not folded into the Fleet tab's read-only overview, a distinct, deliberate choice: "move to the Managers section" meant re-categorising them in the workspace tab bar, not consolidating them into one dashboard. Employees was fully removed from the Manage Users admin panel (no duplicate entry point) once the move landed. See [[Employee Credentials]], [[Plant and Equipment]], [[Vehicle Management]].

**Access side effect, confirmed and kept the same day**: the "management" tab group has no `fieldDefault: true`, so this move also restricted Plant Equipment, Vehicles and Employees to Manager/Admin/Super Admin — "user" and "supervisor" roles no longer see any of the five tabs in this group. This reverses part of the [[Decision Log]]'s 2026-08-06 self-service decision for Plant/Vehicle checkout; the backend callables are untouched and could still serve a self-service UI again if the frontend grouping changes back.

## User Register list (fixed 2026-08-07)

- The list has its own capped-height, independently-scrolling viewport with a sticky column header, rather than requiring a scroll of the whole admin page to reach users further down.
- Clicking the currently-active row now deselects it — the Inspector returns to a neutral "browsing" state instead of being permanently stuck on one user with no way back. Root cause was a `useEffect` that always force-reselected the first user the instant selection went empty, so a genuine "nothing selected" state never used to exist.
- The "Active Users" tile in the admin summary strip now jumps to the User Register on click, matching every other tile in that strip. The Employees tile was removed from this strip the same day once Employees moved to the Project Workspace (see above) — the strip now reads Licence, Seats, Active Users, Enabled Modules, Storage, Region.

