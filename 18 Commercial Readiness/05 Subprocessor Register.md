---
status: draft
updated: 2026-08-08
stage: 15
source: "[[Subprocessor Register]]"
---

# Subprocessor Register

Stage 15 control file.

Detailed register: [[Subprocessor Register]]

## Evidence Checked

- `fibre-gis/src/firebase.ts`
- `fibre-gis/functions/src/friday/fridayConfig.ts`
- `fibre-gis/functions/src/friday/nvidiaClient.ts`
- `fibre-gis/functions/src/index.ts`
- `fibre-gis/src/config/mapTiles.ts`
- `fibre-gis/src/components/map/permits/permitLocationLookup.ts`
- [[Vercel Deployment]]

## Result

Actual providers are identified: Google/Firebase/GCP, Vercel, GitHub, NVIDIA if FRIDAY is enabled, CARTO/OpenStreetMap tiles, Nominatim, optional Street Manager API, and conditional Azure/AWS storage profiles.

Not passed until DPA/contract status, regions, logging retention and international-transfer mechanisms are confirmed.

Priority: P1 before controlled pilot.
