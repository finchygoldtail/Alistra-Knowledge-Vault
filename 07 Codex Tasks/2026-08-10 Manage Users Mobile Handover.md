---
title: Manage Users Mobile Handover
type: codex-handover
status: ready-for-user-test
owner: Alistair
created: 2026-08-10
updated: 2026-08-10
tags: [codex, manage-users, mobile, admin]
---

# Manage Users Mobile Handover

## Objective

Make the existing Manage Users workflow usable for `admin` and `super_admin` users on mobile and narrow tablet screens without changing the backend permission model or creating a second user-management workflow.

## Requirements

- Preserve the existing admin and super-admin role gates, company scoping, user loading, role editing, area access, licence, module and storage actions.
- Keep the full user register table on desktop.
- Provide a touch-friendly mobile user directory with readable identity, role, company, area access and active/inactive state.
- Do not open the first user automatically on mobile.
- Open the existing inspector only after the administrator selects a user, with a clear Back to users action.
- Keep create-user and super-admin company controls usable at phone width.
- Avoid nested interactive controls in user rows.
- Keep the existing Export action functional.

## Files changed

- `C:\Projects\fibre-gis\src\components\admin\UserManagementPanel.tsx`
- `C:\Projects\fibre-gis\src\components\admin\userManagementPanelStyles.ts`

## Decisions made

- Mobile uses a compact card/list presentation while desktop keeps the existing table presentation.
- The inspector follows the mobile user list; secondary area-access and company-policy cards remain after it.
- The existing backend callables and role checks are unchanged.
- Corrected the pre-existing Export button, which was incorrectly wired to close the panel; it now downloads the filtered register as CSV.
- App commit: `8b574ae` — `Fix Manage Users mobile administration flow`.
- GitHub `main`: pushed successfully.
- Vercel production deployment: `dpl_Gd7YRaAuz8jX8X7VTnGumw9bo54B`, `READY`, aliased to `alistragis.com`, `www.alistragis.uk`, `alistragis.co.uk` and the Vercel production aliases.
- Firebase Hosting was not deployed because `fibre-gis-v2.web.app` is redirect-only and does not serve the frontend.

## Tests performed

- `git diff --check` passed.
- Targeted ESLint passed with 0 errors; 8 existing warnings remain in the large panel (unused legacy values, hook dependency warnings and one explicit `any`).
- `npm run typecheck` passed.
- `npm run test:components` passed: 3 files, 8 tests.
- `npm run build` passed.
- Local Vite shell responded at a phone-sized smoke-check URL and produced a local mobile screenshot.
- Vercel last-hour runtime error scan: no runtime errors found.

## Unresolved risks

- Authenticated Manage Users interaction was not completed in an automated browser because the local Chrome runner was blocked by the desktop sandbox profile permission. A real signed-in phone/tablet test is still required.
- The component retains the pre-existing lint warnings listed above; they were not expanded into this scoped mobile fix.
- The mobile breakpoint is the existing `1180px` narrow-layout threshold, so small desktop windows also use the mobile card presentation by design.

## Next recommended action

Run a signed-in test as both an `admin` and `super_admin` on a phone or browser device emulation: open Manage Users, confirm the user cards load, inspect and edit a user, use Back to users, export the filtered register, create a user, and for super-admin switch company.
