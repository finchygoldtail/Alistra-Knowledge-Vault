---
title: Commercial API
type: api
status: live
owner: Alistair
created: 2026-08-07
updated: 2026-08-07
tags: [api, commercial, boq, stock]
---

# Commercial API

Backs [[Commercial Subcontracting]]. Lives in `functions/src/commercial/*` in `fibre-gis`, all callables in `europe-west2`, following the existing per-domain-file convention (mirrors `functions/src/storage/*`). No Postgres/PostGIS — Firestore + Turf.js.

Firestore paths are all under `businesses/{companyId}/...`. Every collection listed here is added to `isServerManagedCollection` (no direct client writes) — see [[Permissions Model]].

## Domains and callables

**Takeoff** (`commercialTakeoffCallables.ts`)
- `runCommercialTakeoff` — measures a boundary polygon against live assets. Points count whole; lines are clipped to their in-boundary length only.
- Collection: `commercialTakeoffs/{id}` + `lines/{id}` subcollection. Read: any business member.

**Material Recipes** (`materialRecipeCallables.ts`)
- `upsertMaterialRecipe`, `createMaterialRecipeVersion` (immutable once created), `listMaterialRecipes`, `getMaterialRecipeVersion`, `retireMaterialRecipe`, `previewRecipeExpansion` (read/compute preview, no persistence).
- Collection: `materialRecipes/{id}` + `versions/{id}`. Read: any business member (materials only, no prices).

**Commercial Packages** (`commercialPackageCallables.ts`)
- `createCommercialPackage`, `updateCommercialPackageDraft` (recipe selections, rate card, excluded asset ids), `lockCommercialPackageSnapshot` (freezes everything into an immutable snapshot; transactionally rejects if any included asset is already committed to a different locked package), `listCommercialPackages`, `getCommercialPackageSnapshot`, `getCommercialPackageCost` (Manager+ only), `compareRateCardsForTakeoff` (pure read/compute, no writes).
- Collections: `commercialPackages/{id}` (open read) → `snapshots/{id}` (open read, frozen quantities/recipe versions/asset geometry, no money) → `costs/{id}` (Manager+ only, the one place money lives on a package).

**Rate Cards** (`rateCardCallables.ts`)
- `upsertRateCard`, `createRateCardVersion` (immutable), `listRateCards`, `getRateCardVersion` — all Manager+ (`requireMarginVisibility`), since these are prices.
- Collection: `rateCards/{id}` + `versions/{id}`. v1 seeded from the pre-existing `RATE_CARD_TSV` via `functions/scripts/seedRateCardV1.ts` (manual, one-off, not deployed).

**Stock** (`stockCallables.ts`)
- `reserveStockForPackage` (only against a locked package; rejects if the package already has an active reservation), `releasePackageStockReservations`, `listStockReservations`.
- Collection: `stockReservations/{id}`. Open read (quantity + material code only, no price). Soft ledger — no warehouse/stock-on-hand integration exists.

**Export** (`commercialExportCallables.ts`)
- `exportCommercialPackageExcel` — generated server-side from the snapshot + costs subdocument only (never live data). Cost sheet included/omitted based on the caller's own role, returned as base64 (no Storage bucket involved).

**Variations & Valuations** (`commercialVariationCallables.ts`, `commercialValuationCallables.ts`)
- `raiseCommercialVariation` (priced at the package's original locked rate card unless an approver explicitly re-prices it), `approveCommercialVariation`, `rejectCommercialVariation`, `listCommercialVariations`.
- `submitCommercialValuation` (sums cost + approved variations only), `certifyCommercialValuation` (separate, `requireCommercialApprover`-gated action — never automatic), `listCommercialValuations`.
- Collections: `commercialPackages/{id}/variations/{id}`, `.../valuations/{id}` — both Manager+ only (`canViewCommercialMoney`), same tier as `costs`/`rateCards`.

**Advisory Change Detection** (`variationDetectionCallables.ts`)
- `detectPackageVariations` — on-demand only, no scheduled job. Re-runs the original takeoff boundary against current assets and diffs against the locked snapshot. Writes suggestions only, never a real variation.
- Collection: `commercialPackages/{id}/suggestedVariations/{id}`. Open read, no money.

**Build Partner Portal** (`buildPartnerCallables.ts` + `buildPartnerAuthContext.ts`)
- Staff-side: `upsertBuildPartner`, `inviteBuildPartnerUser` (creates/links a Firebase Auth account, sets a `buildPartner: {businessId, partnerId}` custom claim — rejects if the email is already linked to a *different* business, enforcing single-business scoping), `listBuildPartners`, `revokeBuildPartnerUser`.
- Partner-side: `listMyAssignedPackages`, `getPackageSnapshotForPartner` — both resolve identity via `resolveBuildPartnerAuthContext`, which never touches `roleGates.ts`/staff role resolution at all (a deliberately separate identity axis) and re-checks a live `active` doc on every call rather than trusting the claim alone (claims can be cached up to an hour).
- Collection: `buildPartners/{id}` + `users/{uid}` — internal-staff-only in Firestore rules; the partner's own client never reads Firestore directly, everything is callable-mediated.
- Frontend: `/partner` route, wired in `src/main.tsx` ahead of `AuthGate` entirely (not inside `App.tsx` — `AuthGate` owns the pre-auth landing page and renders it before `App` ever mounts, so a check inside `App.tsx` never fires for a logged-out visitor).

## Related

- [[Commercial Subcontracting]]
- [[Permissions Model]]
- [[Role Matrix]]
- [[Assets API]]
- [[API Catalogue]]
