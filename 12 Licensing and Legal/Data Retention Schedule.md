---
status: draft
updated: 2026-08-08
stage: 14
related: ["[[03 GDPR Data Register]]", "[[GDPR Responsibilities]]", "[[Backup and Recovery]]", "[[Audit Logging]]", "[[Privacy Notice and Website Legal Notices]]"]
---

# Data Retention Schedule

Stage 14 of the commercial go-live programme. This schedule is based on the code-verified [[03 GDPR Data Register]] and the current `fibre-gis` implementation as inspected on 2026-08-08.

This is an operational engineering draft, not legal advice. The exact periods below must be confirmed by a UK technology solicitor, privacy adviser, accountant, or customer contract as appropriate before they are treated as final commercial terms.

## Current implementation position

The live codebase has deletion actions for some data, but no automated retention enforcement job.

Confirmed from code inspection:

- `deleteLoginUser` deletes a Firebase Auth user plus their root and business profile documents (`fibre-gis/functions/src/index.ts:1920`-`2003`).
- `backupAndDeleteCompany` creates a Storage manifest backup, deletes the business Firestore tree, deletes company Storage files, removes root user docs for that business, and deletes Auth users except the caller (`fibre-gis/functions/src/index.ts:1025`-`1122`).
- `storageProfiles/default` has `backupPolicy.retentionDays` and `dataPolicy.retentionDays` fields, with a default backup retention of 30 days (`fibre-gis/functions/src/storage/storageProfile.ts:20`-`38`, `80`-`101`, `204`-`224`).
- No scheduled Cloud Function (`onSchedule`) or equivalent retention worker was found that reads those fields and deletes expired data. A repo-wide search found only an on-demand variation detector comment explicitly noting no scheduled/background monitor exists (`fibre-gis/functions/src/commercial/variationDetectionCallables.ts:21`-`29`).
- FRIDAY prompt and response text is not retained by the application; only safe audit event names and error codes are logged (`fibre-gis/functions/src/friday/fridayCallables.ts:108`-`178`).

## Files reviewed for this stage

| File | Why it was reviewed | Result |
|---|---|---|
| `fibre-gis/functions/src/index.ts` | User deletion, company deletion, tickets, asset logs and Street Manager request storage | Manual deletion exists for users/company; tickets and logs have no expiry/delete path. |
| `fibre-gis/functions/src/storage/storageProfile.ts` | Retention and backup-policy fields | Retention values are stored/configurable but not enforced by a worker. |
| `fibre-gis/functions/src/storage/storageProfileManagement.ts` | Admin storage profile editing | Admins can set profile policy fields; no retention enforcement found. |
| `fibre-gis/functions/src/friday/fridayCallables.ts` | FRIDAY prompt/log retention | Prompts/replies are sent to NVIDIA only when enabled; app audit logs do not store prompt/reply content. |
| `fibre-gis/docs/BACKUP_RECOVERY_AND_MFA.md` | Backup and restore policy interaction with retention | Backup retention target exists as a runbook, not verified as live cloud configuration. |
| `Alistra Knowledge Vault/12 Licensing and Legal/03 GDPR Data Register.md` | Data categories feeding this schedule | Used as the source map for data types and deletion/export gaps. |

## Retention Schedule

| Data type | Current retention in code | Proposed v1 policy | Deletion method | Technical status | Review needed |
|---|---|---|---|---|---|
| User accounts and login profiles | Until admin deletion | Retain while the user is active, then delete or deactivate when the customer instructs or the account is no longer required | `deleteLoginUser` | Manual action exists; no inactivity cleanup | Customer contract / privacy review |
| Names, emails, roles and permissions | Same as account profile | Same as account profile | `deleteLoginUser` | Manual action exists | Privacy review |
| Root `users/{uid}` mirror docs | Same as account profile | Same as account profile | `deleteLoginUser` and `backupAndDeleteCompany` | Manual action exists; duplicate profile storage should remain consistent | Engineering review for orphan records |
| Support tickets and ticket events | Indefinite | Retain active tickets while open; retain closed tickets only for a defined support/dispute period | No delete-ticket workflow found | Gap: add admin close/archive/delete or retention worker | Legal/support review |
| Site photographs and asset evidence files | Indefinite unless manually deleted | Retain while project evidence is needed; customer-specific retention should be set in contract or storage profile | Normal Storage deletion paths only; no bulk expiry job found | Gap: add lifecycle policy or scheduled cleanup | Customer contract / privacy review |
| Project and map asset data | Indefinite until edited/deleted or company deletion | Retain for active customer projects; export and delete after termination according to contract | Asset edit/delete flows; `backupAndDeleteCompany` for whole company | Partial manual deletion; no project-level retention workflow | Customer contract |
| `assetChangeLogs` | Indefinite | Retain for a defined audit/dispute period, then delete or archive according to legal advice | No delete function found | Gap: append-only design is good for integrity, but unbounded retention needs policy/enforcement | Legal/privacy review |
| `auditEvents` | Indefinite | Retain security/admin events for a defined security/dispute period; avoid normal-user deletion | No delete function found | Gap: no expiry/archive job | Legal/security review |
| Employee records and credential records | Indefinite unless employee deleted | Retain while required for workforce/compliance purposes; delete or archive when no longer needed | `deleteCompanyEmployee` for employee records | Manual action exists; credential/document retention needs confirmation | HR/legal review |
| Vehicle, plant, crew and work-pack operational records | Indefinite unless deleted through feature workflows | Retain while operationally required and for any defect, audit, warranty or dispute period | Existing per-register delete/update functions | Manual actions exist; no age-based cleanup | Commercial/legal review |
| Billing/licence metadata | Indefinite while business record exists | Retain while customer is active and for required accounting/contract period after termination | `backupAndDeleteCompany` | Whole-company deletion exists; no separate billing archive | Accountant/legal review |
| FRIDAY prompts and replies | Not retained by app | Do not retain prompt/reply content in v1 unless a reviewed feature is added | N/A | Already privacy-friendly | Reassess if RAG/chat history is added |
| FRIDAY rate-limit records | Not governed by schedule | Keep only as long as needed for abuse prevention; current window is configurable and defaults to one hour | No cleanup job found | Gap: low-risk small records, but expired docs may accumulate | Engineering review |
| Backups created by company deletion | Stored under `company-backups/{businessId}/{backupId}` | Retain only for a defined protected backup cycle or legal hold | No expiry job found | Gap: backup retention must be implemented, not just documented | Legal/security review |
| Platform/GCP request logs, including possible IP addresses | Not controlled in app code | Follow Google Cloud logging retention and disclose if applicable | GCP Console policy | Not visible from repo | GCP console / DPA review |

## Required Technical Work

| ID | Requirement | Priority | Status | Notes |
|---|---|---|---|---|
| RET-01 | Decide solicitor-approved retention periods for every row above | P1 | Required | The schedule cannot be final until the legal periods are confirmed. |
| RET-02 | Add a retention worker or documented manual runbook for `auditEvents`, `assetChangeLogs`, closed tickets, FRIDAY rate-limit docs and deletion backups | P1 | Required | A policy without enforcement is not enough for commercial readiness. |
| RET-03 | Confirm whether Firebase/GCP native backups and logs have retention policies configured in the console | P1 | Required | Not visible from source. |
| RET-04 | Add an orphan-record check for deleted users referenced by logs, tickets, employee links and asset history | P1 | Required | Deleting the login does not necessarily erase every historical identifier, and some audit retention may be legitimate. |
| RET-05 | Add customer-specific retention fields to onboarding/contracts where customers choose their own project/evidence retention | P1 | Required | Especially important for photographs, audit evidence and project records. |
| RET-06 | Update the privacy notice once periods are confirmed | P1 | Required | The existing privacy notice already references this schedule but still has a completion checkbox. |

## Interim v1 Rule

Until legal review sets exact periods, do not promise fixed deletion timelines to customers beyond what the product can actually perform today. Use contract language that says retention is governed by the agreed Data Retention Schedule, backup cycle, legal obligations and customer instructions.

No commercial go-live should rely on the current retention state as "implemented". The current state is: **policy drafted, partial manual deletion available, automated enforcement not yet implemented**.
