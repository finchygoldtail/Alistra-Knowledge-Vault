---
title: Plant and Equipment
type: feature
status: live
owner: Alistair
created: 2026-08-06
updated: 2026-08-06
tags: [feature, field, assets]
---

# Plant and Equipment

Company-wide register of tools and plant (fusion splicers, OTDR kit, compressors, generators, cable drum trailers, duct rods, winches, vac excavators, mole equipment, gas detectors, lifting gear, traffic management equipment) — one register shared across all projects/areas, not duplicated per area. Each item tracks status, current location, assignment, purchase info, and inspection/service/calibration due dates.

Built 2026-08-06. Firestore: `businesses/{companyId}/plantEquipment/{itemId}`, fully server-managed (Cloud Function callables only, no direct client writes). Client module: `src/modules/plant-equipment/`.

## Field workflow

Any signed-in crew member can scan an item's QR code (or type its asset tag) on a phone/tablet and check it out to themselves or check it back in — this is deliberately self-service, not manager-issued, per the 2026-08-06 decision in [[Decision Log]]. Routine inspections are also self-service; recording a service or calibration (cost/certification data) stays manager+.

## Register management

Managers can add items individually or bulk-add via a downloadable Excel template (mirrors the app's existing template-download pattern used for AG joints/street cabs/address sheets). Compliance alert dashboard surfaces inspections/calibrations due or expired in the next 30 days, and overdue returns.

## Related

- [[Vehicle Management]] — a vehicle's `locationType`/`locationRefId` on plant items records what's stored in which van.
- [[Work Packs]] — work packs can list required plant/equipment.
- [[Permissions Model]]
