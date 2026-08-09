---
title: Vehicle Management
type: feature
status: live
owner: Alistair
created: 2026-08-06
updated: 2026-08-07
tags: [feature, field, assets]
---

# Vehicle Management

Company-wide vehicle register (vans, trucks, trailers, specialist vehicles) with driver handover, mileage tracking, daily checks, defect reporting, and MOT/insurance/road-tax/service compliance alerts.

Built 2026-08-06. Firestore: `businesses/{companyId}/vehicles/{vehicleId}`, fully server-managed. Client module: `src/modules/vehicles/`. Daily vehicle checks reuse the existing Audits Q&A/photo-evidence engine (`vanCheckTemplate`) rather than a new checklist UI, but record the result against the vehicle register directly rather than through `createAssetChangeLog` — that pipeline is for map assets, and a vehicle isn't one.

## Field workflow

Any signed-in team member can record a handover to themselves (self-service, same 2026-08-06 decision as [[Plant and Equipment]]) — this sets the vehicle to "assigned" and stops it showing as available. Explicitly excludes live GPS/location tracking (privacy/consent not reviewed).

## QR-scan checkout (2026-08-07)

Matches Plant & Equipment's existing scan-first flow, using the same extracted shared `QrScanner` component (`src/components/common/QrScanner.tsx` — browser's native `BarcodeDetector` API with manual entry fallback for iOS Safari). Scanning a vehicle's registration looks it up (a new exact-match short-circuit on `listCompanyVehicles`) and lands the driver on the existing handover form, pre-filled but **not auto-submitted** — unlike Plant Equipment's flow, because mileage is a required, driver-entered field a scan can't infer.

## Related

- [[Plant and Equipment]] — "what's stored in this vehicle" is answered by querying plant items whose location points at the vehicle, not a second ownership system, and now surfaced directly in the Management dashboard's Fleet tab (2026-08-07).
- [[Work Packs]] — work packs can list an assigned vehicle.
- [[Permissions Model]]
