---
title: Work Packs
type: feature
status: live
owner: Alistair
created: 2026-08-02
updated: 2026-08-07
tags: [feature, field]
---

# Work Packs

Work packs give field teams the job context, assets, map location, documents and completion requirements for assigned work.

## Smart Work Pack upgrade (2026-08-06)

Extended the existing `WorkPack` record additively with a new `lifecycleStatus` field (draft → awaiting-approval → approved → ready-to-schedule → scheduled, plus a post-completion evidence/QA/handover tail), crew/supervisor assignment, required plant/vehicle/materials, RAMS/permits/drawings attachment, a non-blocking readiness-warning check, and snags. Deliberately left the existing `WorkPackStatus` field (planned/issued/in-progress/complete/carried-over/denied) and the production-logging integration it drives completely untouched — see [[Decision Log]] for why a second orthogonal field was used instead of extending the existing enum.

## Supervisor approval and sign-off (2026-08-07)

Two new callables give the Supervisor role (see [[Role Matrix]]) real write actions instead of just read access: `approveCompanyWorkPackReadiness` (writes `readinessApproval: {approvedAt, approvedByUid}`) and `signOffCompanyWorkPackCompletion` (writes `completionSignOff: {signedOffAt, signedOffByUid}` and sets `handoverStatus: "complete"`). Resolving work-pack snags, previously Manager-only, was also reclassified to Supervisor+.

## Related

- [[Mobile and Tablet Plan]]
- [[Files API]]
- [[Handover]]
- [[Plant and Equipment]]
- [[Vehicle Management]]

