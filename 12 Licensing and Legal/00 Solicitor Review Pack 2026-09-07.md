---
title: AlistraGIS Solicitor Review Pack
status: ready-for-solicitor-review
updated: 2026-09-07
owner: Alistair
related: ["[[Legal Pack Index]]", "[[01 Standard Terms and Conditions]]", "[[02 Software and SaaS Licence Agreement]]", "[[03 GDPR Data Register]]", "[[Data Retention Schedule]]", "[[Subprocessor Register]]", "[[DPIA]]", "[[Data Subject Rights Procedure]]", "[[08 Privacy Notice and Website Legal Notices]]", "[[DPA Requirements]]", "[[Data Breach and Incident Response]]", "[[00 Commercial Readiness Dashboard]]", "[[2026-09-07 Red Item Remediation Update]]"]
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

## 2. 7 September repository-backed remediation result

A fresh review of the current AlistraGIS `main` branch was completed before this pack was finalised. The detailed evidence note is [[2026-09-07 Red Item Remediation Update]].

### Green / evidenced

- Firestore Point-in-Time Recovery and daily Firestore backups are documented as active with 30-day retention.
- A separately verified append-only Storage mirror and an isolated restore test are documented; the managed Firestore restore completed in 627.893 seconds without modifying production.
- The current `main` branch contains a guarded `backupAndDeleteCompany` workflow. For activated companies it collects Firestore/Auth/Storage backup material, writes a restore manifest, recursively deletes the business Firestore tree, deletes company Storage content and removes company Auth users other than the caller, subject to platform-owner/SuperAdmin safeguards and explicit confirmation.
- The storage-profile model exposes `backupPolicy.retentionDays`, `dataPolicy.retentionDays`, `dataPolicy.deletionAfterTerminationDays` and `exportRequiredOnTermination`.
- A repository Cloud Storage lifecycle rule deletes non-current object versions 30 days after they become non-current.
- The incident-response document is no longer empty; an operational runbook has been drafted.

### Amber / implementation or verification remains

- Retention policy/configuration exists but no general application-data retention worker has been evidenced for live tickets, audit events, asset-change logs, evidence files or similar operational records.
- Existing deletion/export capabilities do not yet form one unified per-person DSAR locator/export/erasure workflow across Auth, Firestore, historical references and files.
- Provider DPA/region/log-retention/transfer facts require live account-level verification.
- Wider DR drills and incident-response tabletop/ownership remain.

### Reserved for professional decision

- final retention periods and lawful exceptions;
- controller/processor allocation;
- international-transfer mechanism/wording;
- DPA and privacy-notice approval;
- infrastructure liability caps/exclusions and operational-reliance wording;
- final third-party/API/map licensing interpretation.

## 3. Product and infrastructure risk context

AlistraGIS is not merely a generic office SaaS product. It can hold or display infrastructure/network records, map assets, operational evidence, workforce records, photographs, permits, work packs, audit events and other project information. Planned sectors increase the importance of careful contractual risk allocation because records may relate to telecoms, water, gas, electricity, renewables or wireless infrastructure.

The contracts should make clear, subject to solicitor approval, that the customer owns Customer Data; AlistraGIS retains ownership of its software, APIs, schemas, documentation, designs, methods and improvements; the customer is responsible for the accuracy and lawful supply of Customer Data; AlistraGIS is a system for recording, displaying, managing and analysing information and is not a substitute for statutory searches, engineering verification, safe-working procedures, surveys or other checks required before physical works; maps, imported data, AI-assisted output and network records require appropriate independent verification before operational/safety reliance; and liability caps/exclusions must be appropriate to customer type, contract value and insurable risk.

**Solicitor question:** Are the existing limitation/exclusion provisions enforceable and appropriately drafted for B2B UK infrastructure customers, and should particular losses or safety/utility scenarios have separate caps or carve-outs?

## 4. Data protection role allocation

Working model: for customer-controlled project/workforce/evidence data the customer is normally controller and the AlistraGIS supplier entity normally processor. For AlistraGIS's own account, support, security, licence/billing and vendor records, AlistraGIS is controller where it determines the purposes/means. This is a working engineering/commercial model only.

**Solicitor/privacy questions:** Is this split correct for the proposed service and hosting models? Are there activities where AlistraGIS is an independent or joint controller? Does the proposed DPA adequately cover UK processor requirements? What should change for client-hosted/dedicated deployments?

## 5. Data retention - current technical red

The application now has a clear configuration surface for retention, and non-current Storage versions have a 30-day lifecycle rule, but configuration is not the same as enforcement. No general scheduled retention worker has been evidenced for application records.

Known current position:

- whole-company backup-and-delete is implemented in `main`;
- support tickets/ticket events do not evidence automatic expiry;
- asset-change and audit history require an approved archive/delete/anonymisation policy;
- project/map/evidence records are generally retained until changed/deleted/company deletion;
- FRIDAY prompt/reply content is not retained by the application;
- Firestore scheduled backups are documented with 30-day retention;
- the append-only Storage mirror and tenant-deletion backups require an approved retention/deletion process of their own;
- Google/platform logging retention needs live-account confirmation.

### Engineering that can proceed before legal sign-off

AlistraGIS can build a configurable retention worker that reads approved policy values and initially runs in dry-run/report-only mode. Destructive deletion should not be enabled merely to make the dashboard green. Final periods and exceptions should be approved before they become customer commitments.

**Solicitor questions:** What default periods should apply to each category, which should be customer-configurable, and which categories should be retained or anonymised despite an erasure request for legal/security/audit reasons?

## 6. Data-subject rights, deletion and export - current red/amber

Existing tooling provides strong whole-company exit/deletion capability and partial domain/user deletion/export capabilities, but there is no single DSAR-specific per-person locator/export/erasure workflow.

The required scope includes Firebase Auth, root/business user profiles, tickets/events, asset-change logs, audit events, employee/credential records, vehicle/plant/crew/work-pack references, files/photos and AlistraGIS-controlled billing/licence/support records.

Proposed operational model: identify whether AlistraGIS or the customer is controller for the requested data; verify identity/authority; for customer-controlled data act on documented customer instruction; produce a scoped export rather than an unrestricted tenant dump; delete where permitted and minimise/anonymise retained history where legitimate retention remains; document backup-cycle implications; and record the request, decision, actions and completion evidence.

**Solicitor questions:** Confirm response requirements, verification standard, processor assistance obligations, treatment of audit/safety/contract records, backup handling and wording for the privacy notice/DPA.

## 7. Subprocessors and international transfers

Identified providers include Google Firebase/GCP, Vercel, GitHub, conditional NVIDIA FRIDAY processing, CARTO/OpenStreetMap tile infrastructure and Nominatim, with optional/future Azure/AWS storage and configured Street Manager services.

Firestore production is documented in `europe-west2`, while the production upload bucket and private Storage backup bucket have previously been documented as `US-EAST1`. This must be verified against the live accounts and reviewed before making UK/EU-only residency commitments.

**Solicitor/privacy questions:** Review the supplier/subprocessor chain and transfer mechanisms; advise what must appear in the DPA/privacy notice/subprocessor list; advise on the Storage location once live settings are confirmed; confirm whether NVIDIA requires additional contractual/region controls; and review whether public map/geocoding services are suitable for intended commercial use.

## 8. DPIA and incident response

The engineering-led DPIA has been updated so that backup/restore is no longer described as untested. Key residual privacy risks include cross-tenant access, photographs/evidence, workforce activity, location/geocoding exposure, AI processing, audit logs, support tickets, backups and privileged accounts.

A full incident-response draft now covers cross-tenant disclosure, credential compromise, accidental disclosure/deletion, secret exposure, malicious uploads/abuse, unauthorised exports, deployment/source compromise, subprocessor incidents and availability incidents. It requires incident recording, evidence preservation, containment, scope/data-impact analysis, legal/privacy escalation, notification where required, recovery verification and post-incident corrective action.

Remaining operational work includes incident owner/deputy assignment, a live incident register, contact verification, a tabletop breach exercise and remaining DR drills.

## 9. Backup and recovery evidence

Evidence currently records Firestore PITR; daily Firestore backups with 30-day retention; daily append-only Storage mirror; Storage versioning/soft-delete controls; successful isolated Firestore restore on 11 August 2026; restore duration 627.893 seconds; restored representative business/user/asset/work-pack/ticket/audit/change-log data; production integrity preserved; and security-rule tests after recovery controls.

Residual DR work includes frontend rollback, selective Storage restoration, application cutover to restored database and deputy recovery-owner assignment.

**Solicitor question:** Ensure SLA/RTO/RPO wording does not promise more than tested service-level recovery capability and clarify customer responsibilities for customer-hosted deployments.

## 10. Priority solicitor questions

1. Is the proposed customer-controller / AlistraGIS-processor model correct, and where is AlistraGIS independently a controller?
2. What DPA terms are required for the current hosting, support, security and subprocessor model?
3. What retention periods should be approved by data category, and which records should be anonymised rather than deleted?
4. How should backups, security/audit evidence and legal/accounting records be handled when an erasure request is received?
5. Are the documented provider locations/transfers acceptable once verified, and what transfer mechanism/disclosure is required?
6. Does the DPIA require formal completion before pilot and what changes are triggered by water, gas, power, renewables and wireless LOS expansion?
7. What customer notification/regulatory escalation wording should be included in incident response and contracts?
8. What liability cap/exclusions are appropriate for infrastructure GIS records, and how should the contract state that GIS does not replace statutory searches, surveys or safe-work/engineering verification?
9. Are customer-data ownership, supplier-IP, export and termination/deletion clauses appropriately structured?
10. Do mapping, geocoding, AI and other API licences permit the intended B2B SaaS use?
11. What insurance/liability alignment should be considered for the intended customers and contract values?
12. Which remaining items are must-fix before the first paying customer and which are acceptable for a controlled pilot?

## 11. Documents supplied for review

### Core customer contracts

- [[01 Standard Terms and Conditions]]
- [[02 Software and SaaS Licence Agreement]]
- [[03 Service Level Agreement]]
- [[04 Customer Onboarding Agreement]]
- [[05 Mutual Non-Disclosure Agreement]]

### Privacy and data protection

- [[03 GDPR Data Register]]
- [[Data Retention Schedule]]
- [[Subprocessor Register]]
- [[DPIA]]
- [[Data Subject Rights Procedure]]
- [[08 Privacy Notice and Website Legal Notices]]
- [[DPA Requirements]]
- [[GDPR Responsibilities]]
- [[Data Breach and Incident Response]]
- [[2026-09-07 Red Item Remediation Update]]

### Technical evidence

- [[00 Commercial Readiness Dashboard]]
- [[Stage 20 Backup Implementation]]
- [[Stage 21 Restore Test]]
- [[09 Disaster Recovery Plan]]
- [[Security Overview]]
- [[API Security Assessment]]
- [[Security Remediation]]
- [[Audit Logging]]
- [[Vercel Deployment]]
- [[Firebase Infrastructure]]

## 12. Requested solicitor outputs

Please provide:

1. redline/finalise Standard Terms and SaaS Licence Agreement;
2. confirm/prepare DPA and controller/processor analysis;
3. review Privacy Notice/cookie wording, retention approach, DPIA and incident-response obligations;
4. confirm infrastructure-specific liability and operational-reliance clauses;
5. review third-party/API licensing and international-transfer issues;
6. identify must-fix-before-first-customer items separately from matters acceptable for a controlled pilot.

## Conclusion

AlistraGIS has substantial commercial, privacy and recovery preparation in place. The repository-backed review confirms that the principal technical gap is no longer backup/restore. Remaining engineering/privacy work is retention enforcement, unified per-person DSAR tooling, provider-setting verification and operational exercises. The legal work is now primarily professional validation of policy values, role allocation, contracts, transfers and infrastructure liability rather than drafting from a blank page.
