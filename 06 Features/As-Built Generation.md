---
title: As-Built Generation
type: feature
status: live
owner: Alistair
created: 2026-08-07
updated: 2026-08-07
tags: [feature, field, engineering]
---

# As-Built Generation

Generates as-built documentation from live map state, instead of building it by hand. Manual "Generate As-Built" button, per project/area, in its own workspace tab in the Field group.

Built 2026-08-07. Client module: `src/modules/as-built/`. Runs entirely client-side against already-loaded project assets — no new Cloud Function needed for generation itself.

## Bridges two previously-disconnected engines

- `asBuiltEngine.ts` already did real per-asset status inference and validation, but only ever emitted plain-text sections — no rendering.
- The Job Pack live-map SVG page-paginator (`JobPackLayout.ts`/`JobPackRoutePage.ts`) already did real rendering — live basemap tiles, fibre-colour-coded routes, one page per route with running page numbers, browser print-to-PDF — but only ever consumed `JobPackDocumentModel`, built for Build Partner Job Packs.

Both asset-record types carry a shared `sourceAsset: EngineeringAssetSnapshot` field, which is what makes a thin adapter possible without touching either engine's internals. `src/core/engineering/asBuiltJobPackAdapter.ts`'s `buildAsBuiltJobPackModel()` calls the real as-built inference logic, then maps its output onto `JobPackDocumentModel` field-for-field (severity map: info→info, warning→warning, critical→blocker) and renders it through the existing, unmodified Job Pack paginator with a new `documentLabel` override ("As-Built Record" instead of "Map First Job Pack").

Known, documented simplification: `overheadCables`/`undergroundCables` in the summary default to 0, since as-built generation doesn't currently infer install method per cable — not fabricated data, just an untracked field. Inherits the existing Job Pack ~36-route page cap automatically, since it reuses the same render function unchanged.

## Related

- [[Work Packs]]
- [[Handover]]
- [[Decision Log]]
