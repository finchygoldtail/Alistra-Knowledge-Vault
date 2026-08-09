---
title: Mobile Production Completion and Permit Marker Handover
type: implementation-handover
status: deployed
owner: Alistair
created: 2026-08-09
updated: 2026-08-09
tags: [mobile, production, permits, deployment, handover]
---

# Mobile Production Completion and Permit Marker Handover

## Objective

Add safe field production completion actions to the existing mobile asset workflow and correct the permit-zone map marker to a recognisable UK-style man-at-work sign.

## Requirements delivered

- Cable, duct and joint assets selected from the mobile map can use `PARTIAL COMPLETE` or `COMPLETE IN FULL`.
- Asset type selects the production team automatically:
  - duct → civils or sub-duct
  - cable → cabling or cable blowing
  - joint → splicing
- Full completion calculates existing production first and records only uncovered route gaps or remaining joint splices.
- Joint completion updates production and the asset's complete status in the same asset-set save.
- Completion requests use idempotency keys, save-version conflict checks and server-side user/timestamp fields.
- Backend validates company membership, project/area scope, asset type/team compatibility and crew assignment for field roles.
- Field users receive only the production completion access path; the existing mobile map-editing actions remain disabled.
- Completion audit records include the previous quantity, amount added, new total and completion state.
- The permit map marker and Layers-panel legend now use a clear red/white triangular worker-and-shovel symbol.

## Files changed

Implementation was made in the live `fibre-gis` repository, including:

- `functions/src/storage/mapAssetOperations.ts`
- `functions/src/storage/storageCallables.ts`
- `functions/src/storage/firestoreAssetRepository.ts`
- `functions/src/storage/storageRouter.ts`
- `src/components/Project/workspace/MobileWorkspaceShell.tsx`
- `src/components/Project/workspace/ProjectWorkspaceMobilePanels.tsx`
- `src/modules/production/production.assetActions.ts`
- `src/components/map/layers/AreaPolygonsLayer.tsx`
- `src/components/map/LayersPanel.tsx`
- `tests/production-completion.test.ts`

## Decisions

- This reuses the existing Daily Production backend and records; no second mobile production system was created.
- Managers and admins retain existing wider permissions. Field roles use the narrow completion operation only.
- Existing production writes without an explicit completion mode retain their previous behaviour.
- Firebase Hosting was not used for the frontend because it redirects to Vercel; the frontend was released through the GitHub `main` deployment path.

## Verification

- Commit: `7ac3b4d` — `Add safe mobile production completion workflow`
- GitHub `main`: confirmed at `7ac3b4d`.
- Storage tests: 249 passed.
- Frontend typecheck: passed.
- Frontend production build: passed.
- Functions build: passed.
- Lint: 0 errors; existing repository warnings remain.
- Vercel production deployment: `READY`, aliased to `alistragis.com`, `www.alistragis.uk` and related production domains.
- Firebase project: `fibre-gis-v2`.
- `logCompanyDailyProduction`: `ACTIVE` after deployment.

## Unresolved risks

- Real phone and tablet click-through testing is still required, especially selecting each asset type and testing partial/full completion against existing gaps.
- Firebase's chunked map storage uses save-version conflict protection rather than a single Firestore transaction across every chunk; a conflict is rejected safely, but the storage model remains a future atomicity improvement area.

## Next recommended action

Run the field test scenarios in [[Field Testing Plan]] on a phone and tablet using a cable with gaps, a partly completed duct, and a joint with previous splices. Record any layout or permission issue before the next production change.
