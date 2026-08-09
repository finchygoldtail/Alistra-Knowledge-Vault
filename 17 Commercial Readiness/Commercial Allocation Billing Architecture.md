---
title: Commercial Allocation Billing Architecture
status: in-progress
updated: 2026-08-08
owner: Alistair
tags: [commercial, subcontracting, billing, allocations, gis]
---

# Commercial Allocation Billing Architecture

This note records the safety correction required before AlistraGIS can support real subcontractor billing.

## Core Rule

The saved project boundary is parent project scope only. A subcontractor bill must come from a first-class `CommercialAllocation`; the project boundary must never automatically become a commercial package.

## Implemented in This Slice

- Added server-managed `commercialAllocations` records.
- Added Polygon and MultiPolygon allocation geometry normalization.
- Added server-side intersection of submitted allocation geometry with the saved project boundary.
- Added a map `Commercial Allocation` drawing type using the existing Leaflet drawing infrastructure.
- Added Commercial/BOQ allocation selection and build-partner assignment controls.
- Required `allocationId` for commercial takeoffs; direct project-boundary takeoffs are rejected.
- Added clipped linear segment evidence to takeoff results and package snapshots.
- Replaced line duplicate checks with segment intersection checks; point assets remain ID-conflict protected.
- Added boundary-point flags and blocks package issue until those assets are resolved.
- Added explicit boundary decisions: `allocate`, `exclude`, or `reassign`; unresolved boundary assets stay out of the takeoff and block package issue.
- Added server-side positive-area overlap protection between active allocations in the same project while allowing shared edges.
- Added a 5 cm tolerance to clipped line-segment conflict detection.
- Added contracted -> completed -> submitted -> certified lifecycle enforcement.
- Added completion records validated against the locked snapshot quantities.
- Added immutable allocation revision callable and superseded-revision tracking.
- Added project scope coverage reporting with unallocated-area calculation.
- Extended partner-safe package access through completed, submitted, and certified states.
- Added parent-scope, MultiPolygon, clipped-line, and segment-conflict regression tests.

## Not Yet Complete

- Boundary Allocation Required review queue UI and cross-allocation reassignment workflow.
- Project-level unallocated-scope reporting and map coverage styling.
- Partial-completion editing and evidence review UI; the current BOQ action records full locked-snapshot completion safely.
- Final export verification for completion records, revisions, and certification evidence.
- Live Firebase smoke test and repository-wide lint cleanup remain before deployment.

## Go-Live Position

This correction is **not yet approved for live subcontractor billing**. The main server-side billing gates are now implemented and tested, but deployment remains held pending live Firebase smoke testing, final export verification, and cleanup of the repository-wide lint baseline.

## Source Evidence

- `C:\Projects\fibre-gis\functions\src\commercial\commercialAllocationOperations.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialAllocationCallables.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialTakeoffOperations.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialPackageOperations.ts`
- `C:\Projects\fibre-gis\src\components\Project\workspace\WorkspaceBoq.tsx`
- `C:\Projects\fibre-gis\src\components\JointMapManager.tsx`
- `C:\Projects\fibre-gis\tests\commercial-allocation-operations.test.ts`
- `C:\Projects\fibre-gis\tests\commercial-package-exclusions-and-conflicts.test.ts`
