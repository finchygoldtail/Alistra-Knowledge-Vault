# AlistraGIS Legal, Contract and Commercial Protection Pack

> **Status:** Working drafts for commercial planning and solicitor review. These documents are not a substitute for advice from a qualified solicitor, accountant, employment adviser or data-protection professional.

## Solicitor handover

**Start here:** [[00 Solicitor Review Pack 2026-09-07]]

**Latest compliance action register:** [[16 UK Compliance Action Register 2026-09-08]]

**Latest technical remediation evidence:** [[2026-09-07 Red Item Remediation Update]]

The solicitor review pack consolidates the product/commercial context, current technical evidence, outstanding commercial-readiness risks, privacy/data-protection questions, infrastructure liability issues and the exact documents/questions recommended for professional review. The 8 September compliance register adds the current UK statutory/commercial actions, including the now-live data-protection complaints duty and the new client framework/order structure.

## Core customer contract stack

Recommended structure for new customers:

1. [[13 Client Framework Agreement]] — reusable master commercial/legal framework.
2. [[14 Client Order Form and Service Schedule]] — customer-specific modules, users, projects, hosting, support, implementation and price.
3. [[15 Hosting and Data Responsibility Schedule]] — responsibilities for AlistraGIS-hosted, dedicated and customer-selected hosting.
4. [[02 Software and SaaS Licence Agreement]] — licence grant/use restrictions and software-specific terms.
5. [[01 Standard Terms and Conditions]] — general commercial terms.
6. [[03 Service Level Agreement]] — support/service targets.
7. Signed Data Processing Agreement based on [[DPA Requirements]] where required.

Existing supporting customer documents:

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
- [[12 Data Protection Complaints Procedure]]
- [[DPA Requirements]]
- [[GDPR Responsibilities]]
- [[Data Breach and Incident Response]]
- [[16 UK Compliance Action Register 2026-09-08]]

## Commercial and pricing documents

- [[Client Pricing Pack]] — modular working price book covering modules, seat bands, projects, hosting, support, onboarding, API/AI and examples.
- [[Pricing Models]]
- [[Hosting Options]]
- [[Maintenance and Upgrades]]
- [[API Buyout]]

## Licensing and IP documents

- [[10 Third Party Licence Register]]
- [[11 THIRD_PARTY_NOTICES]]
- [[API Licence Requirements]]
- [[Data Ownership]]
- [[Licensing Options]]
- [[Intellectual Property Index]]

## Required company details before use

Replace all placeholders in square brackets, including legal business name and trading name, company number and registered office, VAT number if registered, contact/legal-notice addresses, data-protection contact, pricing/payment/support terms, hosting model/subprocessors, insurance/liability caps and governing-law/dispute choices.

The current application/legal drafts identify Alistra GIS Ltd and company number 17361925, but the registered-office disclosure remains unresolved because the currently documented address is private residential. This must be resolved before commercial website publication if the business does not want the home address displayed.

## Current professional-review priorities - 8 September 2026

1. Review/finalise [[13 Client Framework Agreement]] and its order/schedule structure.
2. Produce/finalise an execution-ready customer DPA from [[DPA Requirements]].
3. Controller/processor analysis across AlistraGIS-hosted and customer-hosted models.
4. Liability caps/exclusions and operational-verification wording for infrastructure GIS.
5. Approved retention periods and erasure/minimisation treatment for audit, support, workforce and backup records.
6. Subprocessor/region/international-transfer review, including verification of documented Storage location.
7. DPIA review and change triggers for new sectors/AI/location functionality.
8. Incident/breach and statutory data-protection complaint handling obligations.
9. Privacy Notice/cookie publication review against actual production configuration.
10. Third-party map/geocoding/API commercial licensing.
11. Validate [[Client Pricing Pack]] margin, hosting allowances, VAT treatment and discount authority.

## Technical status relevant to legal review

Backup implementation and isolated Firestore restore proof are complete under [[Stage 20 Backup Implementation]] and [[Stage 21 Restore Test]]. Repository review on 7 September also confirmed a guarded whole-company backup-and-delete workflow, explicit retention-policy fields and a 30-day non-current Storage-version lifecycle rule.

The principal remaining technical gap is **retention enforcement and unified per-person DSAR tooling**, followed by live provider-setting verification and operational exercises. Customer-hosted Azure/AWS/PostGIS deployment remains architecturally prepared but not an instant production switch and must pass the acceptance checklist before being sold as live.

## Recommended review order

1. Read [[00 Solicitor Review Pack 2026-09-07]].
2. Read [[16 UK Compliance Action Register 2026-09-08]].
3. Read [[2026-09-07 Red Item Remediation Update]] for current implementation evidence.
4. Review [[13 Client Framework Agreement]], [[14 Client Order Form and Service Schedule]] and [[15 Hosting and Data Responsibility Schedule]] as one contract system.
5. Review SaaS Licence, Standard Terms, DPA requirements and SLA together.
6. Review privacy/data-protection pack and approve/adjust retention, processor and transfer positions.
7. Review infrastructure liability and insurance alignment.
8. Review [[Client Pricing Pack]] alongside accountant/margin assumptions.
9. Review third-party/API licences and IP/brand position.
10. Ask accountant to confirm VAT, revenue recognition, payroll and software-development treatment.

## Version control

Each signed customer contract should record document version, effective date, customer legal name, Order Form/SOW, selected modules, hosting model, licensed users, project allowance, price/renewal date and authorised signatories.
