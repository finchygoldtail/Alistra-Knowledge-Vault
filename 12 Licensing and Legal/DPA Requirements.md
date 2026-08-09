---
status: draft
updated: 2026-08-08
stage: 18
related: ["[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]", "[[DPIA]]", "[[Data Subject Rights Procedure]]", "[[01 Standard Terms and Conditions]]", "[[02 Software and SaaS Licence Agreement]]"]
---

# DPA Requirements

Stage 18 of the commercial go-live programme. This document defines the requirements for a customer Data Processing Agreement for AlistraGIS. It is not the final DPA and must be reviewed or drafted by a UK technology solicitor before commercial execution.

## Files reviewed for this stage

| File | Why it was reviewed | Result |
|---|---|---|
| `Alistra Knowledge Vault/12 Licensing and Legal/01 Standard Terms and Conditions.md` | Existing data-protection and DPA references | Existing terms already say a DPA is needed where supplier processes personal data for the customer. |
| `Alistra Knowledge Vault/12 Licensing and Legal/02 Software and SaaS Licence Agreement.md` | Existing licence obligations | Existing licence references hosting model, backups, exit/export and retention but not a standalone DPA. |
| `Alistra Knowledge Vault/12 Licensing and Legal/03 GDPR Data Register.md` | Processing categories | Supplies data categories and controller/processor assumptions. |
| `Alistra Knowledge Vault/12 Licensing and Legal/Data Retention Schedule.md` | Return/deletion/backup requirements | Supplies current retention and enforcement gaps. |
| `Alistra Knowledge Vault/12 Licensing and Legal/Subprocessor Register.md` | Subprocessor and transfer requirements | Supplies provider list and unresolved DPA/region checks. |
| `fibre-gis/functions/src/storage/storageAccess.ts` and `storageHttpApi.ts` | Technical tenant/security controls | Confirms tenant-scoped access helpers and bearer-token API pattern. |

## Required Parties and Roles

The DPA should identify:

- AlistraGIS / supplier legal entity details;
- customer legal entity details;
- whether the customer is controller, processor or joint controller for each data set;
- AlistraGIS's role as processor for customer project/workforce/evidence data;
- AlistraGIS's controller role for its own account, support, licence and administrative data, if applicable.

## Processing Instructions

The DPA should state that AlistraGIS processes customer personal data only:

- to provide, secure, support and improve the contracted service;
- according to documented customer instructions;
- according to the agreed SaaS licence/order form;
- where required by law, with notice where lawful.

## Subject Matter and Data Categories

The DPA should cross-reference [[03 GDPR Data Register]] and cover:

- user accounts, names, emails, roles and user IDs;
- project, map, operational and audit data;
- photographs, files and site evidence;
- support tickets and ticket events;
- employee/credential data where customers use those modules;
- FRIDAY AI inputs and outputs if enabled;
- licence/billing metadata.

## Data Subjects

Likely data subjects:

- customer employees and contractors;
- AlistraGIS administrators/support contacts;
- field workers;
- build partners;
- individuals incidentally visible in photos/site evidence;
- individuals associated with support or account requests.

## Security Requirements

The DPA should require appropriate technical and organisational measures, including:

- Firebase Authentication and role-based access controls;
- tenant isolation by business/customer;
- server-side authorisation for privileged writes;
- Firestore and Storage security rules;
- server-stamped audit logs for security-critical events;
- secret storage outside source code;
- backup and restore controls;
- incident response and breach notification process;
- least-privilege administrative access;
- secure development and regression testing for permissions.

## Subprocessors

The DPA should incorporate or link the [[Subprocessor Register]] and define:

- current approved subprocessors;
- how customers are notified of new subprocessors;
- objection process and timeline;
- flow-down confidentiality/security/data-protection obligations;
- international-transfer safeguards.

## International Transfers

The DPA should require the relevant UK GDPR transfer mechanism for any processing outside the UK or approved jurisdictions, including SCCs/UK addendum or provider-specific DPA mechanisms as applicable.

Exact provider locations and transfer safeguards must be confirmed for Firebase/GCP, Vercel, NVIDIA, CARTO/OpenStreetMap/Nominatim and any customer-selected Azure/AWS storage provider.

## Data Subject Rights Support

The DPA should require AlistraGIS to assist the customer/controller with:

- access;
- correction;
- deletion/erasure;
- restriction;
- objection;
- portability where applicable;
- locating data across Auth, Firestore, Storage, support tickets, logs and backups.

The operational detail should cross-reference [[Data Subject Rights Procedure]].

## Breach Notification

The DPA should define:

- what counts as a personal data breach;
- how incidents are reported internally;
- notification route to the customer;
- target notification timeline after becoming aware;
- information to be supplied;
- cooperation duties;
- evidence preservation and post-incident review.

Final timing and wording must be solicitor-approved and aligned with [[Data Breach and Incident Response]] once Stage 23 is complete.

## Deletion, Return and Retention

The DPA should cross-reference [[Data Retention Schedule]] and define:

- customer export rights before termination;
- deletion or return of customer data after termination;
- backup retention/expiry;
- legal-hold exceptions;
- handling of audit/security logs;
- customer-hosted versus Alistra-managed storage responsibilities.

## Audit and Assurance

The DPA should define what evidence AlistraGIS can provide:

- security architecture summary;
- current-state validation;
- security test results;
- backup/restore evidence;
- subprocessor register;
- incident-response process;
- external pen-test summary once available.

The DPA should avoid promising ISO 27001 or other certifications unless actually achieved or contractually committed.

## Assistance and Liability Boundaries

The DPA should make clear:

- customer is responsible for the data it chooses to upload and its own lawful basis/retention instructions;
- customer administrators are responsible for role assignment and ordinary-user access within their business;
- AlistraGIS is responsible for platform security controls under its control;
- customer-hosted deployments may shift backup, storage, region and infrastructure responsibilities to the customer.

## Open Items Before Solicitor Review

| ID | Requirement | Status |
|---|---|---|
| DPA-01 | Confirm supplier legal entity and contact details | Required |
| DPA-02 | Confirm final controller/processor split | Required |
| DPA-03 | Confirm subprocessors, regions, DPAs and transfer mechanisms | Required |
| DPA-04 | Finalise retention periods and backup expiry | Required |
| DPA-05 | Complete incident-response and breach procedure | Required |
| DPA-06 | Complete backup/restore evidence | Required |
| DPA-07 | Prepare solicitor review pack containing this document plus the linked registers | Required |
