---
title: AlistraGIS Solicitor Review Pack
status: ready-for-solicitor-review
updated: 2026-09-07
owner: Alistair
related: ["[[Legal Pack Index]]", "[[01 Standard Terms and Conditions]]", "[[02 Software and SaaS Licence Agreement]]", "[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]", "[[DPIA]]", "[[Data Subject Rights Procedure]]", "[[08 Privacy Notice and Website Legal Notices]]", "[[DPA Requirements]]", "[[Data Breach and Incident Response]]", "[[00 Commercial Readiness Dashboard]]"]
---

# AlistraGIS Solicitor Review Pack

**Prepared:** 7 September 2026  
**Purpose:** consolidated briefing for a UK technology/SaaS solicitor reviewing AlistraGIS before a controlled commercial pilot or first paying customer.  
**Status:** engineering/commercial preparation pack. It deliberately identifies matters requiring professional legal judgement rather than presenting them as settled law.

## 1. Executive summary

AlistraGIS is a B2B infrastructure GIS and operations platform currently focused on fibre/telecommunications, with intended sector expansion into water, gas, electricity/power, renewables and wireless point-to-point/line-of-sight infrastructure.

Current documented stack: React, TypeScript and Vite frontend; Leaflet/react-leaflet mapping; Firebase Authentication, Firestore, Storage and Cloud Functions/Google Cloud backend services; Vercel frontend deployment. The product knowledge base is maintained in the Alistra Knowledge Vault/Obsidian and source code is maintained in GitHub.

The intended commercial model is primarily software/SaaS licensing. The working data-role assumption is that customers normally control their own project, infrastructure, workforce and evidence data, while AlistraGIS processes that data to provide the service. AlistraGIS may separately act as controller for its own account administration, support, licence/billing, security and vendor-management data. This role allocation requires solicitor/privacy confirmation.

The legal pack is already substantial. Drafts exist for Standard Terms and Conditions, Software/SaaS Licence Agreement, SLA, Customer Onboarding Agreement, NDA, contractor/employment templates, privacy/website notices, GDPR data register, data retention, subprocessor register, DPIA, data-subject-rights procedure, DPA requirements and third-party/API licence registers.

The principal purpose of solicitor review is therefore **validation and correction of a prepared B2B SaaS/infrastructure legal framework**, not creation from a blank page.

## 2. Commercial readiness position

### Strong/implemented technical evidence

- Customer-data ownership and supplier-IP model is documented in the draft contracts.
- Infrastructure/operational reliance language already requires customers to maintain operational checks and independently verify maps, network records, imported data and AI-assisted outputs before operational reliance.
- GDPR data inventory was created from code-level inspection rather than generic assumptions.
- Unused live-GPS backend functionality was removed after privacy review.
- Current FRIDAY AI implementation is read-only and the application does not retain prompt/reply text in its audit logs.
- Firestore Point-in-Time Recovery is enabled.
- Daily Firestore backups with 30-day retention are active.
- Uploaded files/photos have a separately verified daily append-only Storage mirror.
- An isolated Firestore restore test passed on 11 August 2026 in 10 minutes 27.893 seconds without modifying production.
- Security-rule testing after backup controls recorded 23 Firestore and 10 Storage rules tests passing.

### Matters still requiring implementation or professional confirmation

1. Final data-retention periods and automated/manual enforcement.
2. Per-user DSAR location/export/deletion/minimisation runbook or tooling.
3. Final subprocessor DPAs, regions, log retention and international-transfer position.
4. Formal DPIA/legal privacy review and controller/processor confirmation.
5. Incident-response ownership, notification review and tabletop exercise.
6. Final legal business identity and commercial placeholders throughout customer agreements.
7. Final liability exclusions/caps and infrastructure-risk allocation.
8. Final DPA/customer contract structure.
9. Commercial/API/map provider licence review where public/free services are currently used.

## 3. Product and infrastructure risk context

AlistraGIS is not merely a generic office SaaS product. It can hold or display infrastructure/network records, map assets, operational evidence, workforce records, photographs, permits, work packs, audit events and other project information. Planned sectors increase the importance of careful contractual risk allocation because records may relate to telecoms, water, gas, electricity, renewables or wireless infrastructure.

The contracts should make clear, subject to solicitor approval, that:

- the customer owns Customer Data;
- AlistraGIS retains ownership of its software, APIs, schemas, documentation, designs, methods and improvements;
- the customer is responsible for the accuracy and lawful supply of Customer Data;
- AlistraGIS is a system for recording, displaying, managing and analysing information and is not a substitute for statutory searches, engineering verification, safe-working procedures, surveys or other checks required before physical works;
- maps, imported data, AI-assisted output and network records require appropriate independent verification before operational/safety reliance;
- liability caps/exclusions must be appropriate to customer type, contract value and insurable risk.

**Solicitor question:** Are the existing limitation/exclusion provisions enforceable and appropriately drafted for B2B UK infrastructure customers, and should particular losses or safety/utility scenarios have separate caps or carve-outs?

## 4. Data protection role allocation

### Working model

For customer-controlled project/workforce/evidence data:

- Customer: normally controller.
- AlistraGIS supplier entity: normally processor.

For AlistraGIS's own account, support, security, licence/billing and vendor records:

- AlistraGIS supplier entity: controller where it determines the purposes/means.

This is a working engineering/commercial model only.

**Solicitor/privacy questions:**

1. Is the controller/processor split correct for the proposed service and hosting models?
2. Are there activities where AlistraGIS is likely to be an independent or joint controller despite the customer-owned-data model?
3. Does the proposed DPA adequately cover Article 28/UK requirements for the service?
4. What should change for client-hosted/dedicated deployments?

## 5. Data retention — current red item

The code currently supports some manual deletion but there is no general automated retention worker enforcing the Data Retention Schedule.

Known current position:

- user/Auth/profile deletion exists through `deleteLoginUser`;
- whole-company backup-and-delete exists through `backupAndDeleteCompany`;
- employee and various domain-specific deletion functions exist;
- support tickets/ticket events do not currently have a defined expiry/delete workflow;
- `assetChangeLogs` and `auditEvents` are currently unbounded unless operationally removed;
- project/map/evidence records are generally retained until changed/deleted/company deletion;
- FRIDAY prompt/reply content is not retained by the application;
- Firestore scheduled backups have 30-day retention;
- the append-only Storage mirror is deliberately recovery-safe and needs an approved retention/deletion process of its own;
- Google/platform logging retention needs confirmation from live account settings.

### Proposed policy direction for solicitor review

Do not turn the following into customer promises until approved. Proposed approach:

- active account/profile data: active relationship plus only the period justified after closure/termination;
- closed support tickets: defined support/dispute period;
- audit/security events: defined security/fraud/dispute period, with minimisation/anonymisation where appropriate;
- site photographs and infrastructure evidence: customer-agreed project/evidence period;
- project/map asset data: active project/customer term plus agreed exit/export window, subject to legal holds;
- employee/credential data: customer-defined employment/compliance need and applicable legal obligations;
- billing/contract records: accounting/tax/contract period confirmed by accountant/solicitor;
- backups: documented protected cycle plus legal-hold exception;
- expired rate-limit/temporary security records: short operational period only.

**Solicitor questions:** What default periods should AlistraGIS use for each category, which should be customer-configurable, and which categories should be retained/anonymised despite an erasure request for legal/security/audit reasons?

### Required engineering after legal decision

- implement a scheduled retention worker and/or formally controlled manual runbook;
- enforce expiry for closed tickets, temporary rate-limit records and deletion backups where appropriate;
- implement approved audit/change-log archive/delete/anonymisation policy;
- verify Firebase/GCP log retention and backup lifecycle settings;
- document customer-specific retention choices during onboarding.

## 6. Data-subject rights, deletion and export — current red/amber item

Existing tooling can delete accounts and many domain records, and can export various operational/commercial data, but there is no single DSAR-specific per-user locator/export/erasure tool.

The documented DSAR scope includes Firebase Auth, root and business user profiles, tickets/events, asset-change logs, audit events, employee/credential records, vehicle/plant/crew/work-pack references, files/photos and AlistraGIS-controlled billing/licence/support records.

Proposed operational model:

- identify whether AlistraGIS or the customer is controller for the requested data;
- verify identity/authority;
- for customer-controlled data, act on the customer's documented instruction under the DPA rather than independently deciding the request;
- produce a scoped export, not an unrestricted whole-tenant dump;
- delete where permitted and minimise/anonymise retained history where a legitimate retention requirement remains;
- document backup-cycle implications;
- record the request, decision, actions and completion evidence.

**Solicitor questions:** Confirm statutory response requirements, verification standard, processor assistance obligations, treatment of audit/safety/contract records, backup handling and wording for the privacy notice/DPA.

## 7. Subprocessors and international transfers — current red/amber item

### Confirmed/identified providers

- Google Firebase / Google Cloud Platform — Auth, Firestore, Storage, Functions, Secret Manager and platform logging.
- Vercel — frontend hosting and browser/request delivery.
- GitHub — source code, developer/commit metadata and deployment workflow; production customer data is not intended to be stored there.
- NVIDIA — conditional FRIDAY AI model endpoint when enabled.
- CARTO / OpenStreetMap tile infrastructure — client-side basemap requests.
- OpenStreetMap Nominatim — client-side reverse geocoding for selected coordinates.

### Conditional providers/features

- Microsoft Azure — optional future/customer storage profile.
- AWS — optional future/customer storage profile.
- Street Manager API provider — permit-extension workflow when configured.
- Google Maps — external directions links after user click.

### Important current infrastructure fact

Firestore production is documented in `europe-west2`, but the production upload bucket and private Storage backup bucket are currently documented as `US-EAST1`. This requires explicit privacy/contract/transfer review before commercial commitments about UK/EU-only data residency are made.

**Solicitor/privacy questions:**

1. Review the supplier/subprocessor contract chain and transfer mechanisms.
2. Advise what must appear in the customer DPA/privacy notice/subprocessor list.
3. Advise whether the current US-EAST1 Storage location is acceptable for intended UK customers and what transfer documentation is required.
4. Confirm whether NVIDIA should remain disabled until a suitable DPA/processing-region position is established.
5. Review whether public CARTO/OSM/Nominatim services are suitable for commercial customer use or should be replaced with contracted providers/self-hosted alternatives.

## 8. DPIA — current red item prepared for review

An engineering-led DPIA already exists. Key risks identified include cross-tenant access, photographs/evidence, workforce activity, location/geocoding exposure, AI processing, audit logs, support tickets, backups and privileged accounts.

Privacy-positive controls include removal of unused live GPS, business-scoped storage/access controls, server-side audit work, read-only FRIDAY design and non-retention of FRIDAY prompt/reply content in application logs.

The older DPIA listed backup/restore as incomplete. That factual position is now superseded: backup implementation is complete and an isolated restore test passed. Remaining recovery work concerns wider DR/failover/cutover exercises rather than proving that Firestore backup restoration works.

**Solicitor/privacy questions:**

- Is a formal DPIA mandatory for the current processing, and if so is the engineering-led DPIA a suitable foundation?
- What residual risks/actions must be closed before a controlled B2B pilot?
- What events must trigger a new DPIA (e.g. live worker tracking, AI chat history/RAG, write-capable AI, new utility sectors, sensitive workforce processing)?

## 9. Incident response — Stage 23

A full engineering/operations incident-response draft has now been created at [[Data Breach and Incident Response]]. It covers cross-tenant disclosure, credential compromise, accidental disclosure/deletion, secret exposure, malicious uploads/abuse, unauthorised exports, deployment/source compromise, subprocessor incidents and availability incidents.

The runbook requires incident recording, evidence preservation, containment, scope/data-impact analysis, legal/privacy escalation, customer notification where required, recovery verification and post-incident corrective action.

**Solicitor/privacy questions:** Confirm notification decision process and deadlines, controller/processor communication duties, required customer-contract wording and what incident categories must be reported to customers even where regulatory notification is not required.

## 10. Backup, recovery and disaster recovery

Evidence currently records:

- Firestore PITR enabled;
- daily Firestore backups with 30-day retention;
- daily append-only Storage mirror;
- Storage versioning and soft-delete controls;
- isolated Firestore restore successful on 11 August 2026;
- restore duration 627.893 seconds;
- restored representative businesses/users/assets/work packs/tickets/audit events/change logs;
- production integrity preserved;
- 23 Firestore and 10 Storage rules tests passed after the recovery controls were applied.

Residual DR work includes frontend rollback, selective Storage restoration, application cutover to restored database and deputy recovery-owner assignment.

**Solicitor question:** Ensure SLA/RTO/RPO wording does not promise more than the tested service-level recovery capability and clarify customer responsibilities for customer-hosted deployments.

## 11. Legal entity and contract placeholders

Before signature/publication, the legal pack still needs the final supplier details inserted consistently:

- legal business name/trading name;
- company number;
- registered office;
- VAT number if applicable;
- legal/privacy/support contact addresses;
- pricing/payment terms;
- support hours;
- hosting model;
- named subprocessors;
- insurance levels;
- final liability caps;
- order-form/renewal choices;
- dispute-resolution choices.

**Solicitor task:** perform a consistency review across the Terms, SaaS Licence, DPA, SLA, Onboarding Agreement, Privacy Notice and order-form structure so definitions, precedence, liability, termination, data export/deletion and hosting responsibilities align.

## 12. Intellectual property and third-party licensing

The vault contains an IP/brand section, source-code ownership record, trademark plan/clearance record, third-party licence register, THIRD_PARTY_NOTICES and API licence requirements.

**Solicitor task:** review software/IP ownership chain, customer licence grant, contractor/AI-assisted development implications if relevant, third-party notices, trademark strategy and any restrictions created by mapping/API providers.

## 13. Documents supplied for review

### Core customer contracts

1. [[01 Standard Terms and Conditions]]
2. [[02 Software and SaaS Licence Agreement]]
3. [[03 Service Level Agreement]]
4. [[04 Customer Onboarding Agreement]]
5. [[05 Mutual Non-Disclosure Agreement]]

### Privacy/data protection

6. [[03 GDPR Data Register]]
7. [[Data Retention Schedule]]
8. [[Subprocessor Register]]
9. [[DPIA]]
10. [[Data Subject Rights Procedure]]
11. [[08 Privacy Notice and Website Legal Notices]]
12. [[DPA Requirements]]
13. [[GDPR Responsibilities]]
14. [[Data Breach and Incident Response]]

### Licensing/IP/commercial

15. [[10 Third Party Licence Register]]
16. [[11 THIRD_PARTY_NOTICES]]
17. [[API Licence Requirements]]
18. [[Data Ownership]]
19. [[Licensing Options]]
20. [[Intellectual Property Index]]

### Technical evidence relevant to contractual promises

21. [[00 Commercial Readiness Dashboard]]
22. [[Stage 20 Backup Implementation]]
23. [[Stage 21 Restore Test]]
24. [[09 Disaster Recovery Plan]]
25. [[Security Overview]]
26. [[API Security Assessment 2026-08-08]]
27. [[Security Remediation 2026-08-11]]
28. [[Audit Logging]]
29. [[Vercel Deployment]]
30. [[Firebase Infrastructure]]

## 14. Priority questions for the solicitor

Please prioritise answers to these questions before general drafting polish:

1. Is the proposed B2B customer/controller and AlistraGIS/processor model correct?
2. Is the DPA structure sufficient and what must change?
3. Are the Terms/SaaS liability caps, exclusions and operational-verification clauses suitable for infrastructure GIS use?
4. What default retention periods should be adopted and which must be customer-configurable?
5. How should audit/change logs, support records and backups be treated when erasure is requested?
6. Are the current subprocessors/transfer arrangements suitable, particularly US-EAST1 Firebase Storage and conditional NVIDIA processing?
7. Is a DPIA legally required now and what changes are needed to the existing draft?
8. What incident/breach notification wording and deadlines should appear in the DPA/customer contracts/runbook?
9. What wording is needed to avoid AlistraGIS being treated as a substitute for statutory utility searches, engineering verification or safe-working processes?
10. Are the customer data ownership, supplier IP and exit/export/deletion provisions robust?
11. Are any mapping/geocoding/API licences unsuitable for commercial use?
12. What insurance types/limits should be aligned with the contractual liability caps?

## 15. Recommended review output requested from solicitor

Please provide:

- redline/revised Terms and Conditions;
- redline/revised SaaS Licence Agreement;
- final or model Data Processing Agreement;
- review of Privacy Notice and cookie wording;
- confirmed controller/processor analysis;
- approved/default retention positions or advice on how to set them;
- review of DPIA and incident-response obligations;
- review of liability/risk allocation for infrastructure data;
- review of third-party/API licensing issues;
- list of issues that must be resolved before first paying customer versus issues that may be completed during a controlled pilot.

## 16. Current conclusion

AlistraGIS has substantial legal, security and commercial preparation already documented. The main remaining legal-readiness work is no longer identifying what documents exist; it is **professional validation of the prepared contract/privacy framework and turning approved policy decisions into enforceable operational controls**.

Until that review and the remaining P1 engineering controls are completed, the legal documents should remain marked as drafts and should not be represented as solicitor-approved or final customer terms.
