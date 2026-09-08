---
title: AlistraGIS Customer Data Processing Agreement
status: draft-for-solicitor-review
updated: 2026-09-08
owner: Alistair
related: ["[[13 Client Framework Agreement]]", "[[14 Client Order Form and Service Schedule]]", "[[15 Hosting and Data Responsibility Schedule]]", "[[DPA Requirements]]", "[[03 GDPR Data Register]]", "[[Subprocessor Register]]", "[[Data Subject Rights Procedure]]", "[[12 Data Protection Complaints Procedure]]", "[[Data Breach and Incident Response]]"]
---

# AlistraGIS Customer Data Processing Agreement

> **Draft for solicitor review before signature.** This document is intended to satisfy the customer-controller / AlistraGIS-processor contract requirements for customer-controlled personal data. It must be checked against the current UK GDPR/DUAA position, actual hosting model and final Framework Agreement.

## 1. Parties and incorporation

This Data Processing Agreement (**DPA**) forms part of the contract between:

**Customer:** the customer identified in the applicable Order Form (**Controller**, where it determines the purposes and means of the Customer Personal Data); and

**Supplier:** Alistra GIS Ltd, trading as AlistraGIS, company number 17361925 (**Processor**, where it processes Customer Personal Data on the Customer's behalf).

This DPA is incorporated into the [[13 Client Framework Agreement]] and the applicable [[14 Client Order Form and Service Schedule]].

Where a Party acts as an independent controller for separate processing, that processing is not converted into processor activity merely because this DPA exists.

## 2. Definitions

For this DPA:

- **Applicable Data Protection Law** means the UK GDPR, Data Protection Act 2018, Data (Use and Access) Act 2025 amendments, PECR where applicable, and other binding UK data-protection law relevant to the processing.
- **Customer Personal Data** means personal data processed by AlistraGIS on behalf of the Customer under the contracted service.
- **Data Subject**, **Personal Data**, **Personal Data Breach**, **Processing**, **Processor** and **Controller** have the meanings given by Applicable Data Protection Law.
- **Subprocessor** means another processor engaged by AlistraGIS to process Customer Personal Data for the Customer.

## 3. Scope and processing details

The processing details required for the Order are set out in **Schedule 1** to this DPA and the applicable Order Form.

The Parties must ensure Schedule 1 accurately states:

- subject matter;
- duration;
- nature and purpose;
- categories of personal data;
- categories of data subject; and
- Controller obligations and rights.

## 4. Documented instructions

AlistraGIS will process Customer Personal Data only:

- on the Customer's documented instructions;
- as necessary to provide, secure, support, back up, maintain and administer the contracted service;
- as stated in the applicable Order Form, Framework Agreement and this DPA; or
- where required by UK law, in which case AlistraGIS will inform the Customer before processing unless the law prohibits that notification.

Documented instructions may be contained in the contract, Order Form, authorised support request, configuration selected by the Customer or other written instruction capable of being retained as evidence.

If AlistraGIS believes an instruction infringes Applicable Data Protection Law, it will notify the Customer unless prohibited by law and may pause the affected processing where reasonably necessary while the issue is resolved.

## 5. Confidentiality

AlistraGIS will ensure that persons authorised to process Customer Personal Data are subject to an appropriate duty of confidentiality or equivalent statutory obligation.

Access must be limited to personnel who reasonably require it for their role.

## 6. Security measures

AlistraGIS will implement appropriate technical and organisational measures proportionate to the risks of the processing.

Current controls may include, according to the selected hosting model:

- Firebase Authentication and role-based access;
- tenant/business scoping;
- server-side authorisation for privileged operations;
- Firestore and Storage security rules;
- encryption in transit and provider-managed encryption at rest where applicable;
- restricted privileged administration;
- secret management;
- security/audit logging;
- secure development and regression testing;
- backup and restore controls;
- incident-response processes;
- least-privilege support access.

A more detailed technical/security description may be supplied in **Schedule 2** or supporting security documentation.

The Customer remains responsible for Customer-controlled users, devices, role assignment, source data and Customer-hosted infrastructure as allocated in [[15 Hosting and Data Responsibility Schedule]].

## 7. Subprocessors

The Customer gives **[general / specific — solicitor to confirm preferred mechanism]** written authorisation for AlistraGIS to use the subprocessors listed in [[Subprocessor Register]] or the customer-facing approved subprocessor list.

AlistraGIS will:

- inform the Customer of intended additions/replacements in accordance with the agreed notice mechanism;
- provide a reasonable opportunity to object on legitimate data-protection grounds where general authorisation is used;
- ensure an appropriate written contract is in place with each Subprocessor;
- impose data-protection obligations that provide an equivalent level of protection for the relevant processing; and
- remain responsible for the Subprocessor's performance of its processor obligations to the extent required by law and contract.

The final notice period and objection/remedy process must be completed by the solicitor.

## 8. International transfers

AlistraGIS will not make a restricted transfer of Customer Personal Data except:

- on documented Customer instructions; or
- using a lawful transfer mechanism where required.

Where applicable, this may include UK adequacy regulations, the UK International Data Transfer Agreement, the UK Addendum to approved standard contractual clauses, or another lawful mechanism.

The actual production regions, backup locations, support access and provider chain must be verified before the Supplier makes a contractual UK-only/EU-only data residency commitment.

The Order Form should record any customer-specific residency commitment.

## 9. Data-subject rights assistance

Taking into account the nature of the processing, AlistraGIS will provide reasonable assistance to enable the Customer to respond to requests relating to rights including, where applicable:

- access;
- rectification;
- erasure;
- restriction;
- objection;
- portability; and
- rights concerning automated decision-making.

Operational support is described in [[Data Subject Rights Procedure]].

Where a rights request is received directly by AlistraGIS and concerns Customer-controlled data, AlistraGIS will not independently determine the Customer's controller response unless legally required or separately acting as controller. It will route the request to the authorised Customer contact and provide reasonable processor assistance.

The Parties should define any charge for unusually burdensome assistance beyond ordinary product/support capability in the Framework Agreement/Order Form, subject to legal restrictions.

## 10. Data-protection complaints

AlistraGIS maintains [[12 Data Protection Complaints Procedure]].

Where a complaint concerns Customer-controlled personal data:

- AlistraGIS will identify the relevant Customer/controller;
- preserve relevant evidence;
- route/notify the Customer without undue delay where appropriate;
- assist with investigation according to this DPA; and
- separately handle any processing for which AlistraGIS is itself controller.

The Parties must maintain current privacy escalation contacts in the Order Form.

## 11. Personal data breaches

AlistraGIS will notify the Customer **without undue delay** after becoming aware of a Personal Data Breach affecting Customer Personal Data.

The notification should, to the extent information is available, include:

- nature of the incident;
- categories/approximate number of affected data subjects/records where known;
- likely consequences;
- measures taken or proposed;
- contact/escalation information; and
- further information as it becomes available.

AlistraGIS will take reasonable steps to contain, investigate and remediate the incident and preserve relevant evidence.

The Customer remains responsible for deciding whether and when it must notify the ICO or affected individuals where the Customer is Controller, although AlistraGIS will provide reasonable assistance.

Any contractual customer-notification target shorter than "without undue delay" must be set only after operational and solicitor review.

## 12. Assistance with compliance obligations

Taking into account the nature of processing and information available to it, AlistraGIS will provide reasonable assistance with the Customer's applicable obligations concerning:

- security of processing;
- personal data breach assessment/notification;
- DPIAs; and
- prior consultation with the ICO where required.

AlistraGIS is not responsible for the Customer's independent legal conclusions, lawful bases, privacy notices, employment-law obligations or data-collection decisions unless separately agreed.

## 13. Records and information

AlistraGIS will maintain appropriate records required of it as Processor and provide information reasonably necessary to demonstrate compliance with the processor obligations applicable to the contracted processing.

The Customer may receive relevant evidence such as:

- security architecture summaries;
- applicable security test evidence;
- backup/restore evidence;
- subprocessor information;
- incident-response documentation;
- data-location information available to AlistraGIS;
- processing/data-category records.

Confidential, security-sensitive, third-party or other-customer information may be redacted or provided through an appropriate controlled assurance process.

## 14. Audits and inspections

AlistraGIS will allow for and contribute to reasonable audits/inspections required to demonstrate compliance with applicable processor obligations.

To minimise security risk and disruption, the Parties should normally use a staged assurance process:

1. existing compliance/security documentation;
2. written questions and evidence;
3. remote review/meeting; and
4. on-site or deeper technical inspection only where reasonably necessary.

Audits should be conducted on reasonable notice, during normal business hours, by appropriately qualified persons subject to confidentiality, and without exposing other customers' data or security-sensitive information unnecessarily.

The final audit frequency, cost allocation and urgent-regulatory-exception wording requires solicitor review.

## 15. Retention, return and deletion

At the end of the relevant processing services, and subject to the Customer's choice where applicable, AlistraGIS will return or delete Customer Personal Data and delete existing copies unless UK law requires retention.

The practical process is subject to:

- supported export capability;
- the exit period stated in the Order Form;
- approved retention schedule;
- protected backup cycles;
- legal/security/audit exceptions; and
- Customer-hosted responsibilities.

Where immediate deletion from protected backups is not technically practical, the data must be protected from ordinary use and allowed to expire/delete through the approved backup cycle as documented.

Current retention configuration is not a substitute for actual enforcement. Final periods must be approved before destructive automation is enabled.

## 16. Customer obligations

The Customer will:

- comply with Applicable Data Protection Law as Controller where applicable;
- ensure documented instructions are lawful;
- provide appropriate privacy information and lawful bases to data subjects;
- collect only data reasonably required for legitimate purposes;
- avoid unnecessary special-category/criminal-offence data unless appropriately assessed and controlled;
- maintain accurate authorised-user and role information;
- notify AlistraGIS of relevant privacy/security incidents or rights requests requiring processor assistance;
- provide current controller/privacy escalation contacts.

## 17. Special-category / criminal-offence data

The standard AlistraGIS service is not intended to require routine special-category or criminal-offence personal data.

If a Customer proposes such processing, it must be separately assessed before use, including:

- lawful basis and Article 9/10 conditions where applicable;
- DPIA need;
- access controls;
- retention;
- security;
- contract/insurance impact; and
- any customer/employee transparency requirements.

## 18. AI-assisted processing

Where an AI feature processes Customer Personal Data through a third-party provider, that provider must be approved under the relevant processor/subprocessor and transfer arrangements before the feature is enabled for such data.

The standard DPA does not authorise materially new AI processing such as retained chat history, RAG/document ingestion or write-capable agents unless reflected in the Order Form, Subprocessor Register, DPIA/privacy documentation and processing schedule.

## 19. Customer-hosted deployments

For Customer-selected/customer-hosted infrastructure, this DPA must be read with [[15 Hosting and Data Responsibility Schedule]].

Customer ownership of the infrastructure does not automatically remove AlistraGIS's processor obligations if AlistraGIS still accesses or processes Customer Personal Data.

The Order Form must identify:

- provider/account owner;
- regions;
- who operates backups;
- Supplier access path;
- credential ownership;
- incident responsibilities;
- subprocessor chain; and
- deletion/exit responsibilities.

## 20. Independent-controller processing by AlistraGIS

AlistraGIS may separately act as Controller for its own processing such as:

- account/platform administration where AlistraGIS determines purposes;
- service security and abuse prevention;
- Supplier support/business records;
- licence/billing administration;
- supplier/professional-adviser management;
- statutory/regulatory records.

Such processing is governed by AlistraGIS's applicable Privacy Notice and law rather than the Customer's processor instructions to the extent AlistraGIS independently determines purposes and means.

## 21. Liability and precedence

Liability under this DPA is subject to the liability structure in the Framework Agreement/Standard Terms to the extent permitted by law.

**Solicitor review required** to confirm whether any separate/higher data-protection liability cap, indemnity or carve-out is appropriate.

If this DPA conflicts with another contract document on processing of Customer Personal Data, the agreed order of precedence in the Framework Agreement applies, subject to mandatory law.

## 22. Duration

This DPA starts when AlistraGIS first processes Customer Personal Data under the relevant Order and continues for as long as that processing continues, including any lawful protected backup/retention period after service termination.

## Schedule 1 — Processing Details

Complete per customer/Order.

| Item | Details |
|---|---|
| Customer / Controller | [LEGAL NAME] |
| Processor | Alistra GIS Ltd trading as AlistraGIS |
| Subject matter | Provision of contracted AlistraGIS GIS/infrastructure operations software and selected modules |
| Duration | Subscription term plus approved exit/backup retention cycle |
| Nature of processing | Collection/receipt, hosting, organisation, display, retrieval, transmission where configured, backup, security, support, export, deletion/minimisation as instructed |
| Purpose | Deliver and secure the modules/services specified in the Order Form |
| Data subjects | Customer employees, contractors, field workers, authorised users, build partners, individuals incidentally appearing in evidence/photos, support/account contacts, others specifically authorised by Customer use case |
| Personal data categories | Account identifiers, names, business contact details, roles, user IDs, project/workforce records, audit evidence, photos/files, support information, credentials/training information and other categories actually enabled in the contracted modules |
| Special-category data | Not expected by default; [DETAIL IF APPROVED] |
| Criminal-offence data | Not expected by default; [DETAIL IF APPROVED] |
| Processing locations | [VERIFIED PROVIDERS/REGIONS] |
| Subprocessors | Current approved list / [CUSTOMER-SPECIFIC EXCEPTIONS] |
| Customer instructions | Framework Agreement, Order Form, authorised configuration/support instructions |
| Return/delete choice on exit | [RETURN / DELETE / BOTH PER SCHEDULE] |

## Schedule 2 — Technical and Organisational Measures

Attach/reference the current security schedule and include only controls actually implemented for the selected hosting model.

Minimum headings:

- identity/authentication;
- access control/least privilege;
- tenant isolation;
- encryption/transport security;
- secret management;
- logging/monitoring;
- vulnerability/secure-development process;
- backup/recovery;
- incident response;
- business continuity;
- personnel/confidentiality;
- subprocessor assurance;
- deletion/retention controls;
- customer-hosted responsibility boundaries where applicable.

## Schedule 3 — Approved Subprocessors / Transfers

Use the current [[Subprocessor Register]] or attach a customer-facing version stating:

| Provider | Service | Role | Processing location(s) | Transfer mechanism/status | Customer notice date |
|---|---|---|---|---|---|
| [PROVIDER] | [SERVICE] | [SUBPROCESSOR/OTHER] | [VERIFIED] | [VERIFIED] | [DATE] |

## Signatures

This DPA may be signed as part of the Framework Agreement/Order Form or separately.

### Alistra GIS Ltd
Name: ______________________________  
Title: _______________________________  
Signature: ___________________________  
Date: _______________________________

### Customer / Controller
Legal name: __________________________  
Name: ______________________________  
Title: _______________________________  
Signature: ___________________________  
Date: _______________________________
