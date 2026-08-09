---
title: Main Map
type: frontend
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [frontend, map, leaflet]
---

# Main Map

The map uses Leaflet and react-leaflet. It is the primary interface for geographic work, layer visibility, navigation, measurement and controlled drawing.

## Permission Rules

- Super-admin and admin can draw where allowed.
- Managers, Supervisors and users cannot draw.
- Managers, Supervisors and users may navigate, measure and toggle layers.

## Client Modules layer gating (2026-08-07)

Client Modules entitlements (`clientFeatures`) gate the map's asset layers on two levels:

- **Data**: `applyMapAssetModuleEntitlements()` forces a layer's effective visibility to off when its module is disabled, regardless of the user's own layer-checkbox preference, and blocks selecting/editing that asset type.
- **Sidebar list**: the Layers panel's group list (`LayersPanel.tsx`) is filtered by the same entitlement keys, so a disabled module's layer group disappears from the sidebar entirely instead of sitting there permanently unchecked. Fixed 2026-08-07 after the data-level gating was found to be working correctly but the sidebar list wasn't filtered — see [[Decision Log]].
- Permits, Data Centres, Completed Sections, Status and Measurements have no corresponding Client Modules key and are always shown.

See [[Map API]] and [[Permissions Model]].

