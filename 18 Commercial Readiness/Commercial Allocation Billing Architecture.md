---
title: Commercial Allocation Billing Architecture
status: in-progress-awaiting-live-test
updated: 2026-08-21
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

> Superseded by **Update 2026-08-21** below. Two of the three blockers named
> here are cleared; only the live smoke test remains.

This correction is **not yet approved for live subcontractor billing**. The main server-side billing gates are now implemented and tested, but deployment remains held pending live Firebase smoke testing, final export verification, and cleanup of the repository-wide lint baseline.

## Update 2026-08-21: two of three blockers cleared, and one defect found

### Go-live blockers, re-checked rather than assumed

| Blocker as written 2026-08-08 | Verdict 2026-08-21 |
| --- | --- |
| Repository-wide lint cleanup | **Stale.** 0 errors, and CI has gated on `npx eslint .` since `878b575`. 3438 warnings remain as a baseline, which is not the same thing as a blocker. |
| Final export verification | **Real, and fixed.** See below. |
| Live Firebase smoke test | **Still open.** The only thing now standing between the code and real billing. |

### The export defect

All three things this note asked to verify were genuinely absent from the
package Excel export: completion records, allocation revisions, and
certification evidence. Each has been added — a Completions sheet, a Valuations
& Certification sheet carrying every valuation with who submitted and who
certified, and the allocation revision trail in the summary.

But the thing this note did not name mattered more:

> The summary sheet labelled the snapshot price **"Total Value"**. That is the
> valuation's `baseValue` — the figure *before* approved variations.
> `certifiedValue`, which is what is actually approved for payment and which a
> certifier can override, appeared nowhere in the workbook.
>
> Anyone paying a subcontractor from that spreadsheet would have underpaid by
> the value of every approved variation.

It is now "Contracted Value (snapshot, before variations)", with approved
variations and `CERTIFIED VALUE (approved for payment)` stated separately. A
certifier's override is reported as certified rather than recomputed, because
the approver's figure is the authority.

This became urgent rather than tidy on the same day, when Alistair confirmed a
spreadsheet is the intended output format and no accounting integration is
wanted. It was live billing pointed at the wrong number.

### Subcontractor invoice matching, shipped

Deployed 2026-08-21: `recordSubcontractorInvoice`,
`approveSubcontractorInvoiceForPayment`, `listSubcontractorInvoices`, and a
panel under the valuations list.

Subcontractors send their own invoices; the system records what arrived and
says whether it matches the certified value. It never issues an invoice.

- **One invoice per certified valuation**, enforced inside the transaction that
  writes it, so the same area cannot be paid for twice. The one guard here
  worth calling load-bearing.
- Only a **certified** valuation can be invoiced against. Submitted is a
  request for payment, not an approval.
- **No tolerance band.** A one-penny difference is shown. A mismatch can still
  be approved, but only with a written reason, so the difference lands on the
  record instead of being absorbed.
- An invoice cannot be approved by whoever recorded it, mirroring the existing
  rule for certifying a valuation.
- `certifiedValueAtRecording` is copied onto the invoice, so the record still
  says what was compared if the valuation is ever re-certified.

### Deliberately not built, with the reasoning

The first scoping pass proposed CIS handling, VAT reverse charge, Construction
Act payment notices and generated invoice documents. Alistair pushed back and
was right.

Because the subcontractor issues the invoice, what this produces is an internal
record that goes to nobody — not a tax document — so the content rules
governing a real VAT invoice do not apply to it. CIS is a duty of whoever
actually pays, discharged through whatever already does that today. "CIS may
apply to the business" is not "the software must implement CIS".

**The condition that would change this:** if the system is ever asked to say
what to *pay* rather than whether the invoice is right. That is a different
number, and it is the point at which CIS would have to be modelled.

**Retention is not modelled** because it is held by the client on Harrelli, not
by Harrelli on subcontractors. It belongs to the money-in side.

**Money in — invoicing the client — is not started.** It shares only the
"measure what happened in this area and price it" half, and diverges entirely
after it.

### Revised go-live position

The server-side chain is complete and the export no longer misstates the
figure. What remains before this note can be marked approved for live
subcontractor billing is **one real allocation taken through to a recorded,
approved invoice against live Firebase**. That cannot be done without a real
package and a login, and nothing else substitutes for it.

Full working plan: `docs/INVOICING_BY_AREA_PLAN.md` in the repo.


## Source Evidence

- `C:\Projects\fibre-gis\functions\src\commercial\commercialAllocationOperations.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialAllocationCallables.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialTakeoffOperations.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialPackageOperations.ts`
- `C:\Projects\fibre-gis\src\components\Project\workspace\WorkspaceBoq.tsx`
- `C:\Projects\fibre-gis\src\components\JointMapManager.tsx`
- `C:\Projects\fibre-gis\functions\src\commercial\commercialExportWorkbook.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\subcontractorInvoicePolicy.ts`
- `C:\Projects\fibre-gis\functions\src\commercial\subcontractorInvoiceCallables.ts`
- `C:\Projects\fibre-gis\src\components\commercial\SubcontractorInvoicePanel.tsx`
- `C:\Projects\fibre-gis\docs\INVOICING_BY_AREA_PLAN.md`
- `C:\Projects\fibre-gis\tests\commercial-allocation-operations.test.ts`
- `C:\Projects\fibre-gis\tests\commercial-package-exclusions-and-conflicts.test.ts`
