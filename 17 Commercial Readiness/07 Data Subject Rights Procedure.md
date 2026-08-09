---
status: draft
updated: 2026-08-08
stage: 17
source: "[[Data Subject Rights Procedure]]"
---

# Data Subject Rights Procedure

Stage 17 control file.

Detailed procedure: [[Data Subject Rights Procedure]]

## Evidence Checked

- `fibre-gis/functions/src/index.ts` for profile update/delete, tickets and company delete/backup.
- `fibre-gis/functions/src/storage/*Callables.ts` for entity deletion.
- `fibre-gis/functions/src/commercial/commercialExportCallables.ts` for server-side export.
- Frontend export helpers for client-side exports.
- [[03 GDPR Data Register]].

## Result

Procedure drafted, but implementation incomplete. Existing tooling supports some correction and deletion actions, but no dedicated DSAR register, per-user export helper, erasure/minimisation runbook or central evidence trail exists.

Priority: P1 before controlled pilot.
