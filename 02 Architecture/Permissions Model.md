---
title: Permissions Model
type: architecture
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [permissions, security]
---

# Permissions Model

## Roles

- Super-admin: full platform access, including drawing permissions.
- Admin: company administration and drawing permissions where assigned.
- Manager: may navigate, measure and toggle layers, but cannot draw. Full register/settings access.
- Supervisor (added 2026-08-07): same map access as Manager/User. Approves work-pack readiness, signs off completion, resolves QA flags/snags. Cannot edit registers, delete records, or touch cost/service/calibration/company-wide settings — see [[Role Matrix]].
- User: may navigate, measure and toggle layers, but cannot draw.

## Commercial (added 2026-08-07)

[[Commercial Subcontracting]] introduces a Firestore rule tier between the existing "any active business member" read and "Business Privileged" (Admin+): `canViewCommercialMoney`, gating money-bearing collections (package `costs`, `rateCards`, `variations`, `valuations`) to Manager and above, distinct from quantity-only commercial collections (`commercialTakeoffs`, `materialRecipes`, `commercialPackages`, `stockReservations`) which stay open like the rest of the operational register. See [[Commercial API]], [[Role Matrix]].

## Related Notes

- [[Role Matrix]]
- [[Mobile Permissions]]
- [[API Security]]
- [[Audit Logging]]
- [[Commercial API]]

