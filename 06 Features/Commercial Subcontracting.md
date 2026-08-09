---
title: Commercial Subcontracting
type: feature
status: live
owner: Alistair
created: 2026-08-07
updated: 2026-08-07
tags: [feature, commercial, boq, stock]
---

# Commercial Subcontracting

Map-driven commercial subcontracting: select or draw an area on the map, measure it, expand it into materials, price it against a rate card, lock it into an immutable package, assign it to a Build Partner, export it, and track variations/valuations against it. "The map is the commercial source" — quantities come from the network itself, not a manually rebuilt spreadsheet.

Built in `fibre-gis` (the live app), not `AlistraGIS` (the architecture-rewrite scaffold) — confirmed via that repo's own `START_HERE.md`, which explicitly says not to touch Map/Production/Assets/Firestore there yet. See [[Decision Log]].

## Workflow

Map selection → spatial takeoff → asset recipes (sundries) → rate card pricing → commercial package (locked snapshot) → Build Partner assignment → Excel export → variations/valuations → advisory change detection.

## What got built (2026-08-07)

Ten phases, all live in `functions/src/commercial/*` and wired into the existing **Commercial**/**BOQ** Project Workspace tabs (`WorkspaceBoq.tsx`) rather than a new surface — see [[Commercial API]] for the full endpoint/entity list.

- **Spatial takeoff**: points count whole if inside the drawn/selected boundary; lines (duct/cable) are clipped to only the length actually inside — never counted at full stored length. Uses Turf.js server-side (added as a `functions` dependency), not the dormant PostGIS path already in the backend — Firestore + Turf was the deliberate choice here, no new database infrastructure.
- **Material recipes**: versioned, admin-authored rules (exact/per-asset/per-metre/percentage/manual) expand a measured quantity into sundries (glands, kits, labels, waste allowance). Immutable once created — a locked package keeps using the version it was locked against.
- **Commercial packages**: freeze a takeoff + recipe selections + a geometry COPY of every included asset into an immutable snapshot at lock time. Later map/recipe/rate-card edits can never retroactively change what a locked package says it covers.
- **Build Partner portal**: a separate `/partner` route (bypasses the internal staff login entirely — different identity axis via a Firebase custom claim, not a new role tier), single-business scoped by design (a partner working for two clients gets two separate logins, not one spanning both).
- **Rate cards**: versioned pricing, migrated from the pre-existing hardcoded `RATE_CARD_TSV` in `exportBoqExcel.ts` as v1 (one-off script, `functions/scripts/seedRateCardV1.ts` — not run automatically). Cost computed at lock time into a separately-gated subdocument.
- **Exclusions + duplicate-allocation protection**: per-asset exclusion before locking; a transactional check rejects locking a package if any of its assets are already committed to a different **locked** package. Deliberately id-based, not true sub-line geometric overlap (documented as a conscious over-blocking simplification).
- **Stock reservation**: a soft ledger only — not tied to any warehouse/inventory system, since none exists in this codebase.
- **Excel export**: generated server-side from the frozen snapshot only, never live data. Whether the cost sheet is included depends on the *caller's actual role*, not a client-supplied flag.
- **Variations & valuations**: a variation is priced at the package's originally-locked rate card unless an approver explicitly re-prices it. Valuation submission and certification are two separate, differently-privileged actions — production completion status is never read by either, so it can't accidentally authorise payment.
- **Rate-card comparison**: price one takeoff against multiple rate cards side by side, pure read/compute, no writes — for comparing Build Partners before committing.
- **Advisory change detection**: on-demand only (this codebase has no scheduled/triggered Cloud Functions anywhere — adding the first one felt like a bigger change than this one feature needed). Re-runs the original takeoff boundary against the current map and diffs it against the locked snapshot. Writes suggestions only; never creates or edits a real variation itself.

## Permissions

New gates in `functions/src/commercial/commercialRoleGates.ts`, following the existing [[Role Matrix]] convention of separate, non-parameterised helpers rather than one parameterised function:

- `requireCommercialManager` — package/recipe/rate-card creation and editing. Excludes User, Supervisor.
- `requireCommercialApprover` — package locking, variation approval, valuation certification. Excludes User, Supervisor, **and Manager** — one tier above ordinary commercial management, since these are commitment actions.
- `requireMarginVisibility` — read gate for cost/rate/margin data specifically, independent of the write gates.

Firestore rules: every new collection is added to `isServerManagedCollection` (no direct client writes anywhere). Money-bearing collections (`costs`, `rateCards`, `variations`, `valuations`) get a new `canViewCommercialMoney` rule (Manager+), distinct from the open-to-any-business-member read the quantity-only collections (`commercialTakeoffs`, `materialRecipes`, `commercialPackages`, `stockReservations`) get.

## Known simplifications (deliberate, not oversights)

- Duplicate-allocation protection is id-based, not true sub-line geometric overlap — two genuinely non-overlapping segments of one long duct asset would currently be (over-)flagged as a conflict.
- Change detection is on-demand (a button), not a scheduled background sweep.
- Stock reservation has no link to a real warehouse stock-on-hand figure.
- No "reason" field is captured when excluding an asset from a package.

## Related

- [[Commercial API]]
- [[BOQ and Stock]]
- [[Role Matrix]]
- [[Permissions Model]]
- [[As-Built Generation]]
- [[Decision Log]]
