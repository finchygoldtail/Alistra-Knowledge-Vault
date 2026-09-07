# AlistraGIS Legal, Contract and Commercial Protection Pack

> **Status:** Working drafts for commercial planning and solicitor review. These documents are not a substitute for advice from a qualified solicitor, accountant, employment adviser or data-protection professional.

## Solicitor handover

**Start here:** [[00 Solicitor Review Pack 2026-09-07]]

**Latest technical remediation evidence:** [[2026-09-07 Red Item Remediation Update]]

The solicitor review pack consolidates the product/commercial context, current technical evidence, outstanding commercial-readiness risks, privacy/data-protection questions, infrastructure liability issues and the exact documents/questions recommended for professional review. The 7 September remediation note records the repository-backed distinction between implemented controls, engineering work still required and matters deliberately reserved for professional judgement.

## Core customer documents

- [[01 Standard Terms and Conditions]]
- [[02 Software and SaaS Licence Agreement]]
- [[03 Service Level Agreement]]
- [[04 Customer Onboarding Agreement]]
- [[05 Mutual Non-Disclosure Agreement]]
- [[06 Contractor Agreement]]
- [[07 Employment Contract Template]]
- [[08 Privacy Notice and Website Legal Notices]]
- [[09 Accountant Appointment and Finance Setup]]

## Privacy and data-protection documents

- [[03 GDPR Data Register]]
- [[Data Retention Schedule]]
- [[Subprocessor Register]]
- [[DPIA]]
- [[Data Subject Rights Procedure]]
- [[DPA Requirements]]
- [[GDPR Responsibilities]]
- [[Data Breach and Incident Response]]

## Licensing and IP documents

- [[10 Third Party Licence Register]]
- [[11 THIRD_PARTY_NOTICES]]
- [[API Licence Requirements]]
- [[Data Ownership]]
- [[Licensing Options]]
- [[Intellectual Property Index]]

## Required company details before use

Replace all placeholders in square brackets, including legal business name and trading name, company number and registered office, VAT number if registered, contact/legal-notice addresses, data-protection contact, pricing/payment/support terms, hosting model/subprocessors, insurance/liability caps and governing-law/dispute choices.

## Current professional-review priorities - 7 September 2026

1. Controller/processor analysis and final DPA structure.
2. Liability caps/exclusions and operational-verification wording for infrastructure GIS.
3. Approved retention periods and erasure/minimisation treatment for audit, support, workforce and backup records.
4. Subprocessor/region/international-transfer review, including verification of documented Storage location.
5. DPIA review and change triggers for new sectors/AI/location functionality.
6. Incident/breach notification obligations and customer-contract wording.
7. Privacy Notice/cookie publication review against actual production configuration.
8. Third-party map/geocoding/API commercial licensing.

## Technical status relevant to legal review

Backup implementation and isolated Firestore restore proof are complete under [[Stage 20 Backup Implementation]] and [[Stage 21 Restore Test]]. Repository review on 7 September also confirmed a guarded whole-company backup-and-delete workflow, explicit retention-policy fields and a 30-day non-current Storage-version lifecycle rule.

The principal remaining technical gap is **retention enforcement and unified per-person DSAR tooling**, followed by live provider-setting verification and operational exercises. Final retention values, role allocation, transfer mechanisms, DPA wording and infrastructure liability remain professional legal/privacy decisions.

## Recommended review order

1. Read [[00 Solicitor Review Pack 2026-09-07]].
2. Read [[2026-09-07 Red Item Remediation Update]] for current implementation evidence.
3. Confirm business structure and ownership of software/source code.
4. Review customer-facing Terms, SaaS Licence, DPA requirements, SLA and onboarding structure together.
5. Review privacy/data-protection pack and approve/adjust retention, processor and transfer positions.
6. Review infrastructure liability and insurance alignment.
7. Review third-party/API licences and IP/brand position.
8. Ask accountant to confirm VAT, revenue recognition, payroll and software-development treatment.

## Version control

Each signed customer contract should record document version, effective date, customer legal name, Order Form/SOW, hosting model, licensed users, price/renewal date and authorised signatories.
