---
title: Map Asset Storage Audit 2026-08-19
type: architecture-assessment
status: accepted
owner: Alistair
created: 2026-08-19
updated: 2026-08-19
tags: [architecture, firestore, storage, cost, map-assets]
---

# Map Asset Storage Audit 2026-08-19

## Outcome

A concern that clients were driving high Firestore read/write volume was investigated and found to be unfounded at current scale. A read-only audit callable, `auditCompanyMapAssets`, was built and deployed to `fibre-gis-v2` to measure it rather than estimate it. Every company is clean and small. The planned map asset re-sharding was consequently **shelved with a documented trigger rather than implemented**, since applying it now would increase cost rather than reduce it.

Two real duplication defects were found and closed along the way, and one emulator-only defect that had been blocking local QA of the Management dashboard.

## Measured position

| Company | Clean | Chunk docs | Assets | Distinct ids | Size |
| --- | --- | --- | --- | --- | --- |
| `fibre-gis-v2` | yes | 1 | 27 | 27 | 49 KB |
| `harrelli comms` | yes | 1 | 56 | 56 | 108 KB |

No duplicate chunk indices, no duplicate asset ids, no unparseable chunks, no orphans, in either.

With one chunk per company a save rewrites that chunk plus two metadata documents — roughly three writes. Modelled against two users saving continuously through a working month, that is approximately **12p per month**. There is no cost problem to solve.

The `1300+ assets` figure in the autosave comment in `useMapAutosave.ts`, which originally motivated the concern, is around sixteen times the real production volume.

## Why sharding was shelved

The legacy layout numbers chunk documents by an asset's **position in the array**, so inserting one asset near the front shifts every later asset into a different chunk and the whole project is rewritten. The planned fix derives the document from a hash of the asset id instead, making placement stable so an edit dirties exactly one document.

That only pays off across many chunks. Both companies span one. Sharding 83 assets into the minimum eight shards would turn one document write into several — strictly worse.

The design, the migration sequence and the hash are written up in `docs/MAP_ASSET_SHARDING_PLAN.md` in the repository, and the foundation (placement, sizing, per-asset signature diffing, fifteen tests pinning the hash to canonical vectors) is built and committed but not wired into any save path.

**Trigger to revisit: any single company passing roughly 1,500 assets** (~10 chunks, ~12 writes per save). Re-run the audit to check; it is read-only.

## Defects closed

1. **Duplicate chunk documents at the same index.** `chunk_0` and `chunk_00000` both resolve to index 0, and the reader loaded both and concatenated their contents. Every writer in the codebase zero-pads; the source of the unpadded form was the emulator seed script. Compounding: a load returning an asset twice was saved back twice, so a project grew on every save cycle. One seeded polygon reached eleven copies locally. Reader now collapses duplicate indices to the zero-padded document; seed script fixed.
2. **No de-duplication by asset id.** `loadSplitMapAssets` has always de-duplicated by id; the main chunk path never did, which is what allowed the above to compound rather than stay flat. Repeated ids are now dropped on load with a warning, and the repair persists on the next save.
3. **`admin.firestore.<Static>` undefined under the Functions emulator.** `getCompanyManagementAnalytics` threw `Cannot read properties of undefined (reading 'documentId')`, surfaced in the UI as a bare `INTERNAL Retry` on Management → Areas. Not a production fault: firebase-tools replaces `require.cache["firebase-admin"]` with a proxy whose `getOriginal()` returns `value.bind(target)` for non-constructor functions, and `bind` does not copy own properties, so every static hanging off `admin.firestore` is lost. This affected **47 call sites across 11 files**, mostly `FieldValue.serverTimestamp()` and `arrayUnion()` on vehicle, equipment, employee and work-pack writes — the analytics call was simply the first path exercised. All converted to deep imports from `firebase-admin/firestore`. Recorded in `docs/LOCAL_EMULATOR_QA.md`.

Production data was audited after these fixes and is clean, so no repair pass is required.

## Correction worth carrying forward

Client-side save improvements made during this work (batched writes, trimming the split mirror to the single bucket actually read, removing a duplicate parent-document read) apply to the **client** path in `src/services/mapAssetStorage.ts`.

Production does not use that path. `isBackendStorageApiEnabled()` defaults to true, so saves route through the backend API to the **server-side** repository in `functions/src/storage/firestoreAssetRepository.ts`. Confirmed empirically: the split-bucket mirror has never run in production, because the server path does not have one.

The server repository still carries a duplicate `mapAssets/main` read per save and no de-duplication of either kind. Neither is urgent while the data is clean, but the de-duplication is cheap insurance against the compounding failure mode and should be ported when that file is next touched.

## Related

- [[Data Storage Strategy]]
- [[Cost and Abuse Protection]]
- [[Architecture Overview]]
- [[Active Bugs]]
