---
title: BOQ and Stock
type: feature
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [feature, boq, stock]
---

# BOQ and Stock

BOQ and stock workflows track materials, quantities, usage and reporting.

## Real backend added (2026-08-07)

The BOQ/Stock tab's rate card, quantities and stock counts were entirely `localStorage`-backed until now (`modules/boq/boq.api.ts` — per-browser, no server persistence). [[Commercial Subcontracting]] gives this a real backend: material recipes, versioned rate cards, and stock reservation, all via [[Commercial API]]. The existing tab and its paste-from-Excel conventions were kept; the new callables were wired in alongside, not replacing the UI.

## Related

- [[Commercial Subcontracting]]
- [[Commercial API]]
- [[Assets API]]
- [[Daily Production]]
- [[Reporting]]

