---
title: Field Testing Plan
type: testing
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-09
tags: [testing, field]
---

# Field Testing Plan

Field testing validates mobile and tablet workflows for real delivery conditions.

## Scenarios

- Open assigned [[Work Packs]].
- Complete audit through [[Audits API]].
- Upload production evidence through [[Production API]].
- Navigate on [[Main Map]].

## Mobile production completion checks

- Select a duct from the map and confirm the production action opens with civils/sub-duct selected automatically.
- Select a cable and confirm cabling/cable blowing is derived from the asset, without a manual category choice.
- Select a cable or duct with existing gaps and use `COMPLETE IN FULL`; verify only the gaps are recorded and the total reaches 100%.
- Select a partly completed joint and verify only the remaining splice count is recorded and the joint becomes complete.
- Repeat a completion action or refresh during submission; verify no duplicate production record is created.
- Confirm a field user can record production but cannot open map drawing/editing actions.
- Confirm the permit marker is a clear triangular man-at-work sign on the map and in the Layers panel.
