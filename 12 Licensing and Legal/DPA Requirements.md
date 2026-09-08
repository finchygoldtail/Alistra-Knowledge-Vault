---
status: implementation-requirements-complete-draft-created
updated: 2026-09-08
stage: 18
related: ["[[17 Customer Data Processing Agreement]]", "[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]", "[[DPIA]]", "[[Data Subject Rights Procedure]]", "[[12 Data Protection Complaints Procedure]]", "[[13 Client Framework Agreement]]", "[[15 Hosting and Data Responsibility Schedule]]"]
---

# DPA Requirements

Stage 18 of the commercial go-live programme. This document records the requirements used to build [[17 Customer Data Processing Agreement]]. The DPA draft now exists, but it remains subject to UK technology/privacy solicitor review before commercial signature.

## Current position — 8 September 2026

**Requirement definition:** substantially complete.  
**Execution-ready legal document:** draft created, solicitor review required.  
**Technical/privacy dependencies:** retention, live subprocessor/provider verification, DSAR tooling and final controller/processor allocation remain partly open.

## Core Article 28 requirement set

The customer DPA must accurately include:

- subject matter and duration of processing;
- nature and purpose of processing;
- types of personal data;
- categories of data subject;
- Controller obligations and rights;
- processing only on documented Controller instructions unless law requires otherwise;
- confidentiality obligations;
- appropriate technical and organisational security measures;
- Subprocessor authorisation and equivalent contractual protections;
- assistance with data-subject rights;
- assistance with security, breach, DPIA and prior-consultation obligations where applicable;
- return/deletion of personal data at end of processing, subject to lawful retention and protected backup cycles;
- information needed to demonstrate compliance; and
- audits/inspections.

These requirements are now reflected in [[17 Customer Data Processing Agreement]].

## Role allocation

Working model for solicitor confirmation:

- Customer normally Controller for its project/workforce/evidence/operational personal data;
- AlistraGIS normally Processor for that data where it hosts/processes it to supply the service;
- AlistraGIS may separately be Controller for its own account administration, security, support, licence/billing, supplier and business-management records.

The hosting model does not alone decide the role. Customer-hosted infrastructure can change the processor/subprocessor chain without automatically removing AlistraGIS processor obligations.

## Processing scope

The DPA/Order Form should cover only processing actually enabled for the customer, potentially including:

- user accounts, names, emails, roles and user IDs;
- project/map/operational data;
- audit/change records;
- photographs/files/site evidence;
- support/complaint/rights-request information;
- employee/credential information where those modules are used;
- AI inputs/context only where contractually enabled and provider checks are complete;
- licence/billing metadata where AlistraGIS processes it as Controller rather than Processor.

## Security requirements

The DPA should point to actual controls, including where relevant:

- Firebase Authentication and role-based access;
- tenant isolation/business scoping;
- server-side authorisation for privileged operations;
- Firestore/Storage rules;
- security/audit logging;
- secret management;
- backup/restore controls;
- incident response;
- least-privilege administration;
- secure development/regression testing.

Do not promise certifications such as ISO 27001 or Cyber Essentials unless actually achieved.

## Subprocessors and transfers

The DPA must link to the current [[Subprocessor Register]] and state:

- authorisation mechanism;
- customer notice process for additions/replacements;
- objection/remedy process;
- equivalent flow-down obligations;
- international-transfer safeguards where needed.

Live region/DPA/log-retention/transfer verification remains outstanding for relevant providers before final customer residency promises are made.

## Rights and complaint assistance

The DPA must support:

- [[Data Subject Rights Procedure]] for access/correction/erasure/restriction/objection/portability; and
- [[12 Data Protection Complaints Procedure]] for complaints concerning customer-controlled data.

The Customer remains responsible for Controller decisions where it is Controller; AlistraGIS assists according to the DPA.

## Breach notification

The DPA draft now uses **without undue delay** as the baseline Customer notification obligation after AlistraGIS becomes aware of a breach affecting Customer Personal Data.

A shorter contractual target should be inserted only after confirming it can be operationally met and after solicitor review.

## Deletion, return and retention

The DPA must work with [[Data Retention Schedule]] and the selected hosting model to define:

- export/return rights;
- deletion/return at service end;
- protected backup cycle;
- lawful-retention exceptions;
- audit/security record handling;
- customer-hosted deletion responsibilities.

Retention configuration fields are not sufficient unless operational enforcement/process exists.

## Audit and assurance

The DPA draft uses a staged assurance model:

1. existing documentation/evidence;
2. written questions;
3. remote review;
4. deeper/on-site inspection where reasonably necessary.

Final frequency, notice and cost allocation require solicitor review.

## Current open items

| ID | Requirement | Status |
|---|---|---|
| DPA-01 | Supplier legal identity/company number | Complete — Alistra GIS Ltd / 17361925 |
| DPA-02 | Registered office/legal-notice address | Required before signature/publication |
| DPA-03 | Final controller/processor split | Solicitor/privacy review |
| DPA-04 | Subprocessors, regions, DPAs and transfer mechanisms | Live verification required |
| DPA-05 | Final retention periods and enforcement | Required |
| DPA-06 | Incident-response process | Drafted; tabletop/owner/deputy pending |
| DPA-07 | Backup/restore evidence | Complete for current evidenced scope |
| DPA-08 | Customer DPA document | Draft created — [[17 Customer Data Processing Agreement]] |
| DPA-09 | Customer-hosted responsibility model | Draft created — [[15 Hosting and Data Responsibility Schedule]]; technical validation pending |
| DPA-10 | Solicitor redline/approval | Required before commercial signature |

## Professional review questions

1. Is the default Controller/Processor split correct across each hosting model?
2. Is general Subprocessor authorisation appropriate, and what notice/objection period should apply?
3. Does the audit clause appropriately balance Article 28 rights with multi-tenant security/confidentiality?
4. Should there be a separate/higher liability cap for data-protection/confidentiality matters?
5. What transfer language is needed once provider regions/mechanisms are verified?
6. What retention/deletion exceptions should apply to security/audit, backup and dispute records?
7. Should the DPA impose a specific contractual processor-to-controller breach notification target shorter than "without undue delay"?
8. Are any additional terms needed for workforce data, photographs, infrastructure records or future AI processing?
