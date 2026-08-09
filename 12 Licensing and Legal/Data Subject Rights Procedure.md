---
status: draft
updated: 2026-08-08
stage: 17
related: ["[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[DPIA]]", "[[Subprocessor Register]]", "[[Privacy Notice and Website Legal Notices]]"]
---

# Data Subject Rights Procedure

Stage 17 of the commercial go-live programme. This is the operational procedure for handling access, correction, deletion, restriction, objection and portability requests involving AlistraGIS data.

This is an engineering and operations draft. It must be reviewed against the customer DPA, final privacy notice and solicitor advice before commercial use.

## Files reviewed for this stage

| File | Why it was reviewed | Result |
|---|---|---|
| `fibre-gis/functions/src/index.ts` | User profile update/delete, tickets, company delete/backup and asset logs | Confirms `updateLoginUserProfile`, `deleteLoginUser`, `backupAndDeleteCompany`, ticket flows and log loaders. No full DSAR export/delete workflow found. |
| `fibre-gis/functions/src/storage/*Callables.ts` | Entity-level deletion and operational records | Confirms some delete functions exist for crews, employees, plant, vehicles, documents and work packs; no unified per-user erasure/minimisation. |
| `fibre-gis/functions/src/commercial/commercialExportCallables.ts` | Server-side commercial Excel export | Export is role-gated and logged, but is not a DSAR export. |
| `fibre-gis/src/services/csvExport.ts` and frontend export helpers | Client-side export behaviour | Several exports happen in-browser and are not centrally DSAR-scoped or audit-logged. |
| `Alistra Knowledge Vault/12 Licensing and Legal/03 GDPR Data Register.md` | Data locations to search | Used as the DSAR search scope. |

## Role Split

For customer project/workforce data, the customer business is expected to be the controller and AlistraGIS the processor. In that case, AlistraGIS should not independently decide whether to fulfil or refuse a request; it should assist the customer/controller according to the DPA.

For AlistraGIS's own platform administration, support, licence and vendor records, AlistraGIS may be the controller and should handle requests directly.

## Intake Channels

Requests may arrive by email, support ticket, direct customer contact, or customer administrator escalation. All requests should be logged with:

- request date;
- requester name and contact;
- data subject name/contact, if different;
- customer/business involved;
- request type;
- identity/authority verification status;
- due date;
- decision and outcome;
- staff member handling the request.

## Identity and Authority Verification

Before disclosing, deleting or exporting personal data:

- Verify the requester controls the relevant email/account, or obtain confirmation from the customer administrator if the data belongs to a customer-controlled tenant.
- If the requester acts for someone else, require evidence of authority.
- For employee/workforce data, route through the customer's authorised administrator unless the DPA says otherwise.
- Do not disclose another user's account, project, audit or ticket data to an ordinary user merely because they ask for "all company data".

## Request Handling

| Right | Operational process | Current tooling | Gap |
|---|---|---|---|
| Access | Identify whether request concerns AlistraGIS controller data or customer-controlled data. For customer data, ask the customer/controller to approve scope before export. | Admins can view user profiles; specific data can be queried/exported manually by authorised admin/developer. | No dedicated DSAR export tool. |
| Correction | Correct account profile fields, role/permission errors, ticket details or customer records through existing admin/product workflows. | `updateLoginUserProfile` exists for user profiles; many domain records have upsert flows. | No central correction register. |
| Deletion / erasure | Determine whether deletion is legally allowed or whether records must be retained for audit, contract, safety, accounting or dispute reasons. | `deleteLoginUser`, domain delete functions and `backupAndDeleteCompany` exist. | No per-user erasure workflow across audit/ticket/history references. |
| Restriction | Suspend/deactivate account or restrict processing scope while a dispute is resolved. | User profile has `active` flag; licence/business controls exist. | No formal restriction workflow or status register. |
| Objection | Assess basis and customer/controller instructions. Stop non-essential processing where appropriate. | Feature flags/licence controls can disable some functions. | Requires legal/customer decision; no product-level objection workflow. |
| Portability | Provide structured data where applicable and technically feasible. Avoid exporting whole-tenant data to ordinary users. | Some CSV/Excel/report exports exist, but many are client-side and not DSAR-scoped. | No DSAR-specific portable export. |

## Search and Export Scope

A DSAR search may need to check:

- Firebase Authentication user record;
- root `users/{uid}`;
- `businesses/{businessId}/users/{uid}`;
- support tickets and ticket events created by or mentioning the user;
- `assetChangeLogs`;
- `auditEvents`;
- employee records and credential records;
- vehicle/plant/crew/work-pack records referencing the user;
- uploaded files/photos where the user is identifiable or named;
- billing/licence/support records controlled by AlistraGIS.

FRIDAY prompt/reply text is not retained in the current implementation, so there is no chat transcript to export or erase unless that feature changes later.

## Deletion Rules

Deletion should be specific and evidenced:

- Delete authentication/profile records when an account is no longer needed and no retention reason applies.
- Do not blindly delete audit logs that are needed for security, fraud, contractual dispute or compliance evidence.
- Where audit/event history must remain, consider minimisation/anonymisation after the approved retention period rather than full immediate deletion.
- Backups may retain deleted data until the approved backup retention cycle expires; this must be explained in the privacy notice and DPA.

## Ordinary User Export Restriction

Ordinary users must not be given a bulk export of organisation data. Organisation-level export should require customer administrator approval and should be logged as a sensitive action.

## Response Targets

Use the legally required response period once confirmed by solicitor/DPO. Until confirmed, treat all rights requests as urgent operational requests and track due dates manually.

## Required Technical Work

| ID | Requirement | Priority | Status |
|---|---|---|---|
| DSR-01 | Create a DSAR/request register template or support-ticket category for privacy requests | P1 | Required |
| DSR-02 | Add an admin-only per-user data locator/export helper, or a documented manual query runbook | P1 | Required |
| DSR-03 | Add a per-user deletion/minimisation runbook covering profile docs, Auth, tickets, employee links, logs and backups | P1 | Required |
| DSR-04 | Log organisation-level exports as security-sensitive events | P1 | Required |
| DSR-05 | Update privacy notice with the final request channel and verification approach | P1 | Required |

## Current Stage Result

Procedure drafted, but **not fully implemented**. Existing admin/delete capabilities cover some requests, but a commercial pilot still needs a proper request register, export/deletion runbook and customer-controller approval process.
