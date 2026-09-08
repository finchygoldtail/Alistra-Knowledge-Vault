---
status: operational-draft-for-professional-review
updated: 2026-09-08
stage: 17
related: ["[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[DPIA]]", "[[Subprocessor Register]]", "[[08 Privacy Notice and Website Legal Notices]]", "[[12 Data Protection Complaints Procedure]]"]
---

# Data Subject Rights Procedure

Stage 17 of the commercial go-live programme. This is the operational procedure for handling access, correction, deletion, restriction, objection and portability requests involving AlistraGIS data.

This is an engineering and operations draft. It must be reviewed against the customer DPA, final privacy notice and solicitor advice before commercial use.

## Current legal timing baseline — updated 8 September 2026

For a subject access request, the current ICO position is that AlistraGIS/controller must respond **without undue delay and within one month** of receipt, subject to the rules on identity, authorised representatives, clarification and any permitted fee.

Where necessary because a request is complex or a person has made a number of requests, the response period may be extended by **up to a further two months**. If an extension is used, the person must be informed and told why within the initial one-month period.

The Data (Use and Access) Act 2025 also makes clear that an organisation must perform a **reasonable and proportionate search** for requested information rather than an unlimited/disproportionate search.

Where clarification is reasonably required for a SAR, the one-month period may pause in accordance with the current ICO right-of-access guidance. Do not use clarification merely to delay or force a person to narrow a valid request.

Other individual rights may have their own rules/exceptions; the solicitor/privacy adviser should confirm any right-specific handling not covered in this operational procedure.

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

Requests may arrive by email, support ticket, direct customer contact, social media or customer administrator escalation. A request does not have to use the words "subject access request" or quote legislation to be valid.

All requests should be logged with:

- request date;
- requester name and contact;
- data subject name/contact, if different;
- customer/business involved;
- request type;
- identity/authority verification status;
- statutory due date;
- extension/clarification status where applicable;
- decision and outcome;
- staff member handling the request;
- linked complaint/incident reference where relevant.

## Identity and Authority Verification

Before disclosing, deleting or exporting personal data:

- Verify the requester controls the relevant email/account, or obtain confirmation from the customer administrator if the data belongs to a customer-controlled tenant.
- If the requester acts for someone else, require proportionate evidence of authority.
- For employee/workforce data, route through the customer's authorised administrator unless the DPA says otherwise.
- Do not disclose another user's account, project, audit or ticket data to an ordinary user merely because they ask for "all company data".
- Only request formal ID where reasonably necessary; avoid excessive identity collection.

## Request Handling

| Right | Operational process | Current tooling | Gap |
|---|---|---|---|
| Access | Identify whether request concerns AlistraGIS controller data or customer-controlled data. For customer data, ask the customer/controller to approve scope before export. Make a reasonable and proportionate search. | Admins can view user profiles; specific data can be queried/exported manually by authorised admin/developer. | No dedicated DSAR export tool. |
| Correction | Correct account profile fields, role/permission errors, ticket details or customer records through existing admin/product workflows. | `updateLoginUserProfile` exists for user profiles; many domain records have upsert flows. | No central correction register. |
| Deletion / erasure | Determine whether deletion is legally allowed or whether records must be retained for audit, contract, safety, accounting or dispute reasons. | `deleteLoginUser`, domain delete functions and `backupAndDeleteCompany` exist. | No per-user erasure workflow across audit/ticket/history references. |
| Restriction | Suspend/deactivate account or restrict processing scope while a dispute is resolved. | User profile has `active` flag; licence/business controls exist. | No formal restriction workflow or status register. |
| Objection | Assess basis and customer/controller instructions. Stop non-essential processing where appropriate. | Feature flags/licence controls can disable some functions. | Requires legal/customer decision; no product-level objection workflow. |
| Portability | Provide structured data where applicable and technically feasible. Avoid exporting whole-tenant data to ordinary users. | Some CSV/Excel/report exports exist, but many are client-side and not DSAR-scoped. | No DSAR-specific portable export. |

## Search and Export Scope

A DSAR search may need to check, where relevant and proportionate:

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

## Third-party and other-person information

Before disclosure, assess whether records contain personal data about other people, customer-confidential information, legally privileged material, security-sensitive information or another applicable exemption/restriction.

Do not provide an unrestricted tenant dump merely because it is technically easier. Provide the requester's personal information and required supplementary information in a secure and appropriate format.

## Deletion Rules

Deletion should be specific and evidenced:

- Delete authentication/profile records when an account is no longer needed and no retention reason applies.
- Do not blindly delete audit logs needed for security, fraud, contractual dispute, legal obligations or compliance evidence.
- Where audit/event history must remain, consider minimisation/anonymisation after the approved retention period rather than full immediate deletion.
- Backups may retain deleted data until the approved backup retention cycle expires; this must be explained in the privacy notice and DPA.
- Record why data was retained where an erasure request is not fully granted.

## Ordinary User Export Restriction

Ordinary users must not be given a bulk export of organisation data. Organisation-level export should require customer administrator approval and should be logged as a sensitive action.

## Response and Communication Rules

- Record the due date as soon as a request is recognised.
- Begin locating information promptly rather than waiting until the deadline approaches.
- Respond without undue delay.
- For SARs, use the one-month statutory deadline as the ordinary maximum.
- Where a permitted extension is necessary, notify the requester within the initial month and explain why.
- Provide information securely and in a commonly used electronic format where the request was made electronically unless another lawful/appropriate format is agreed.
- Where a request is refused or only partly fulfilled, provide the required explanation and complaint/ICO route as applicable.
- If a requester is dissatisfied with handling, route the matter through [[12 Data Protection Complaints Procedure]].

## Required Technical Work

| ID | Requirement | Priority | Status |
|---|---|---|---|
| DSR-01 | Create a DSAR/request register template or support-ticket category for privacy requests | P1 | Required |
| DSR-02 | Add an admin-only per-user data locator/export helper, or a documented manual query runbook | P1 | Required |
| DSR-03 | Add a per-user deletion/minimisation runbook covering profile docs, Auth, tickets, employee links, logs and backups | P1 | Required |
| DSR-04 | Log organisation-level exports as security-sensitive events | P1 | Required |
| DSR-05 | Update privacy notice with the final request channel and verification approach | P1 | Required |
| DSR-06 | Add due-date, extension, clarification and outcome fields to the privacy request register | P1 | Required |
| DSR-07 | Run a mock SAR end-to-end and record evidence before first ordinary paying customer | P1 | Required |

## Current Stage Result

Procedure updated for the current 2026 timing/search rules, but **not fully implemented**. Existing admin/delete capabilities cover some requests, but a commercial launch still needs a proper request register and a tested export/deletion/minimisation runbook. A single automated DSAR button is not itself a legal requirement; a documented, controlled manual workflow can be used where it reliably meets the applicable deadlines and security requirements.
