---
title: Map Performance Work 2026-09-10
type: feature
status: shipped
owner: Alistair
created: 2026-09-10
updated: 2026-09-10
tags: [map, performance, firestore, change-set, deployment]
related: ["[[Maintenance and Upgrades]]", "[[Hosting Options]]", "[[Data Licensing and Custody Options]]", "[[02 Architecture]]"]
---

# Map Performance Work — 10 September 2026

> **Live in production, both halves, as of 10 September 2026.**

## 1. The complaint

The map slowed down as jobs and assets were added, and it got worse when several people worked the same area.

## 2. What was actually wrong

Three sessions had blamed the database, then the network. Both were wrong. Hooking `JSON.parse` in the running app and recording where each call came from found the real cause in minutes.

**The cost was never the reload. It was whole-array work on the client, on every save by anybody.**

1. Every client watches one document, `businesses/{id}/mapAssets/main`. Any save bumps a version number on it, every watching client sees that, and every one of them reloaded the entire estate.
2. On applying those assets, the client compared old and new state by **deep-cloning every asset and serialising both arrays**.
3. Worse, a "persist project" effect deep-cloned *and* re-parsed the geometry of every asset to build an object whose asset list was then deliberately thrown away.

Item 3 was the bulk of it. Pure waste, running on every change.

## 3. Measured, before and after

Watcher browser, a colleague renaming one pole, 2,000-asset estate:

| | JSON work | Operations |
|---|---:|---:|
| Before | 4,578 KB | 4,244 |
| After | **2.2 KB** | **2** |

Roughly a **2,000-fold reduction** in the work every other person's browser does when somebody saves. Verified in the running application, with the data correct afterwards.

## 4. Real estate size, measured

A read-only census script now exists (`scripts/audit-map-asset-counts.mjs`), because the backend audit function had no caller — no button, no script — so the recorded figures had gone stale.

| Company | Assets | Payload |
|---|---:|---:|
| harrelli comms | **1,200** | **3.03 MB** |
| fibre-gis-v2 | 0 | — |

Growth: **56 assets on 19 August → ~370 in early September → 1,200 on 10 September.** Roughly tripling weekly. Assets average 2.6 KB, which is heavy — detailed chambers and many-vertex ducts.

**Run `node scripts/audit-map-asset-counts.mjs` weekly.** It is read-only and takes seconds. This number drives storage allowances in [[Data Licensing and Custody Options]] and should be watched against the 100 GB included allowance.

## 5. What was built

| Piece | State |
|---|---|
| Change set — the server records exactly what each save touched | Built, tested, **backend not deployed** |
| `loadCompanyMapAssetsByIds` — serves only the changed assets | Built, **not deployed** |
| Client patches instead of reloading | **Live** |
| Clone/serialise fix — the 2,000× win | **Live** |
| Partial-save guard and shard storage | Built and tested, **deliberately not wired in** |

Everything fails safe. If the change set is incomplete, the client is more than one save behind, an asset is missing or the network fails, the client falls back to a full reload — the behaviour that existed before.

Tests: **1,353 pure tests and 34 emulator tests, all passing.**

## 6. Two architectural facts worth recording

**The backend callable is the live save path.** `isBackendStorageApiEnabled()` defaults true and nothing sets it false, so map saves go through the `saveCompanyMapAssets` Cloud Function, **not** the client-side storage module. The shelved sharding plan in `docs/MAP_ASSET_SHARDING_PLAN.md` targets the client path and would not have affected production as written. That document needs rewriting before anyone follows it.

**Asset geometry is not GeoJSON.** `geometry.coordinates` is stored `[latitude, longitude]`, the reverse of the GeoJSON standard, and every reader in the codebase expects that. Any importer, exporter or future PostGIS migration that trusts the field name will silently relocate the entire network into the Indian Ocean. This is the concrete form of the geometry risk flagged in the PostGIS audit.

## 7. Deployment — done

Frontend shipped via `git push origin main` (Vercel, commit `a735a6f`). Backend deployed by name on 10 September:

- `loadCompanyMapAssetsByIds` — created
- `saveCompanyMapAssets`, `loadCompanyMapAssets`, `upsertCompanyMapAsset`, `deleteCompanyMapAsset` — updated

Both verified live and correctly refusing unauthenticated calls. **The patching path is now switched on for real customers.**

```
npx firebase-tools deploy --only "functions:loadCompanyMapAssetsByIds,functions:saveCompanyMapAssets,functions:loadCompanyMapAssets,functions:upsertCompanyMapAsset,functions:deleteCompanyMapAsset" --project fibre-gis-v2
```

Deployed by name rather than all at once, to stay within quota.

## 8. Also found, not fixed

**A stale derived layout can make the platform under-report an estate.** A state was reached where the parent record said 150 assets while storage held 2,000. No data was lost, and it was not caused by this work — the code already warns about it (`assembled 2000 assets but its index records 150`). But once a company falls into it, every read returns the subset and looks perfectly self-consistent.

Same family as the "Blockage asset was not found" bug. **Worth its own session**, and worth knowing about before a customer sees it.

## 9. Commercial relevance

- Multi-user performance is now a selling point rather than a risk. Several people working one area was the worst case; it is now the ordinary case.
- The census gives a real basis for storage allowances and overage pricing.
- The 3.03 MB estate at 1,200 assets is a useful sizing datapoint: the 100 GB included allowance in Model A is not close to being a constraint at current volumes.
- The customer-hosted position is unchanged — still fail-closed, still not live. See [[Data Licensing and Custody Options]] section 5.

## Related

- [[Maintenance and Upgrades]]
- [[Hosting Options]]
- [[Data Licensing and Custody Options]]
- [[Client Pricing Pack]]
