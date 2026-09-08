---
title: AlistraGIS UK Compliance Action Register
status: live-working-register
updated: 2026-09-08
owner: Alistair
related: ["[[Legal Pack Index]]", "[[12 Data Protection Complaints Procedure]]", "[[Data Subject Rights Procedure]]", "[[17 Customer Data Processing Agreement]]", "[[DPA Requirements]]", "[[DPIA]]", "[[08 Privacy Notice and Website Legal Notices]]", "[[13 Client Framework Agreement]]", "[[Client Pricing Pack]]"]
---

# AlistraGIS UK Compliance Action Register — 8 September 2026

> This register separates what AlistraGIS **actually needs**, what is already in place, what still needs implementation, and what is not currently required. It is an engineering/commercial compliance register, not a substitute for solicitor, accountant or ICO advice.

## Status key

- **GREEN** — substantially in place/evidenced.
- **AMBER** — required/relevant and partly complete.
- **RED** — required/relevant action outstanding before ordinary commercial launch.
- **NOT CURRENTLY REQUIRED** — reassess if scope changes.

## Current register

| Area | Need? | Status | Current position / action |
|---|---|---|---|
| UK GDPR / Data Protection Act compliance | Yes | AMBER | GDPR data map, DPIA, rights procedure, retention and security material exist. Final legal role/lawful-basis/retention/transfer review remains. |
| ICO data-protection fee | Almost certainly yes for current controller activities unless an exemption is confirmed | RED — external action | AlistraGIS acts as controller for some of its own account/support/security/licensing/business data. Complete ICO self-assessment and register/pay appropriate tier. Current ICO Tier 1 fee is £52, £5 discount by Direct Debit. |
| Privacy Notice | Yes | AMBER | Draft updated 8 Sep 2026 with legal entity/company number, complaints duty and current SAR position. Registered office, final retention values and live provider/transfer facts remain before publication. |
| Data Processing Agreement | Yes where AlistraGIS processes personal data for customer/controller | AMBER | [[17 Customer Data Processing Agreement]] now exists as a full working draft. Solicitor redline/approval plus final role, subprocessor, transfer and retention facts remain. |
| Data-protection complaints process | Yes — statutory duty in force | GREEN/AMBER | [[12 Data Protection Complaints Procedure]] added 8 Sep 2026. In-app/support complaint category, owner/deputy and end-to-end test remain. |
| Subject access / individual-rights process | Yes | AMBER | Procedure updated for current one-month SAR timing, permitted extensions and reasonable/proportionate search. Unified per-person locator/export/minimisation tooling remains desirable. |
| Data retention schedule | Yes | AMBER | Policy/config exists. General application-data enforcement remains incomplete. Do not invent expiry periods simply to close the item. |
| Record of processing / data register | Required/recommended for current recurring processing | GREEN | [[03 GDPR Data Register]] is detailed and code-backed. Keep it current as modules/providers/data categories change. |
| Subprocessor register | Yes for customer/processor transparency and DPA operation | AMBER | Register exists. Live DPA, region, logging and transfer facts still require account-level verification. |
| International-transfer review | Yes where data/access leaves UK adequacy scope | AMBER | US-region Storage/provider facts need live verification; document applicable transfer mechanism before making residency promises. |
| Personal-data breach/incident procedure | Yes | AMBER | Runbook exists. Assign incident owner/deputy, maintain incident register, verify contacts and run tabletop exercise. |
| DPIA | Sensible and may be mandatory for high-risk features | AMBER | Engineering-led DPIA exists. Professional review remains; reassess on live worker tracking, AI history/RAG/write agents and new high-consequence sectors. |
| Formal statutory DPO | Not currently evidenced as mandatory | NOT CURRENTLY REQUIRED | Current B2B SaaS scope does not by itself demonstrate large-scale systematic monitoring or large-scale special-category processing. Nominate an internal privacy lead; reassess if scope changes. |
| Cookie consent banner | Not for current essential-only/non-tracking configuration | NOT CURRENTLY REQUIRED | Current technical/legal audit records no active advertising/marketing/analytics tracker requiring consent. Keep cookie/device-storage notice and reassess before adding non-essential tracking. |
| Cookie/device-storage notice | Yes/recommended | AMBER | Privacy/legal draft now records current essential-only position; final production technology verification remains. |
| Registered company details on website | Yes for company website/business communications | RED — external/site action | Website/business materials need full legal company disclosure including registered office. If current address is private residential, arrange an appropriate public registered-office service before publication if desired. |
| Terms / SaaS licence | Commercially essential | AMBER | Drafts exist; now supplemented by [[13 Client Framework Agreement]], Order Form, Hosting Schedule and customer DPA. Solicitor redline required. |
| Client Framework Agreement | Commercially essential for proposed sales model | AMBER | Draft added 8 Sep 2026; modular Order Form controls modules, seats, projects, hosting and support. Liability/dispute wording requires solicitor. |
| Client Order Form | Yes for modular contracting | GREEN/AMBER | Template added 8 Sep 2026. Needs final commercial/legal approval and quote process. |
| Hosting/data responsibility schedule | Yes for mixed hosting options | GREEN/AMBER | Template added 8 Sep 2026. Customer-hosted production still requires technical validation before general sale. |
| Pricing pack | Commercially required | GREEN/AMBER | Working modular pricing pack and quote template added 8 Sep 2026. Validate margin/infrastructure allowances before public publication. |
| SLA | Not statutory but commercially important | AMBER | Draft exists. Do not promise recovery/availability beyond tested capability. |
| Cyber Essentials | Not a general legal requirement | NOT CURRENTLY REQUIRED | Consider when customer procurement, insurance or public-sector work makes it valuable. |
| ISO 27001 certification | Not a general legal requirement | NOT CURRENTLY REQUIRED | Do not state or imply certification. Consider later if enterprise procurement justifies cost. |
| Accessibility statement | Not currently treated as a primary legal go-live blocker for private B2B app | OPTIONAL/AMBER | Accessibility work remains good practice and customer procurement may impose standards. |
| Trade mark registration | Not mandatory | COMMERCIAL | Separate IP/brand protection work already exists. |

## Immediate actions before first ordinary paying customer

1. **Complete ICO fee self-assessment and pay/register if required.**
2. **Have solicitor finalise the Framework Agreement, SaaS/Terms and [[17 Customer Data Processing Agreement]] as one coherent contract set.**
3. **Finish the Privacy Notice with the approved registered-office address, final retention and verified provider details.**
4. **Implement the privacy/data-protection complaint intake category and register.**
5. **Run a mock SAR and build/document the per-person locator/export/minimisation workflow.**
6. **Approve retention values and build/report retention enforcement before destructive automation.**
7. **Verify provider regions, subprocessors, DPAs, logging retention and international transfers.**
8. **Resolve website/company disclosure address.**
9. **Run incident-response tabletop and assign deputy.**
10. **Validate Client Pricing Pack margins and cloud/storage allowances before publishing externally.**

## Controlled pilot position

A controlled pilot may be lower risk than a full public commercial launch where:

- test/demo data is used where possible;
- live personal/customer-sensitive data is not loaded until DPA/privacy/security checks are complete;
- hosting model is the currently supported production model unless customer-hosted acceptance testing has passed;
- scope/modules/users are explicitly limited in a Pilot Order;
- no unsupported SLA, data residency or security certification promise is made.

## Change triggers requiring compliance review

Reopen this register when AlistraGIS introduces:

- live worker GPS or systematic location monitoring;
- biometric or special-category data workflows;
- criminal-offence data;
- AI chat history/RAG/customer-document ingestion;
- write-capable AI agents;
- new marketing analytics/ad tracking;
- new cloud/provider/region;
- new customer-hosted architecture;
- material expansion into water, gas, electricity/power or other safety-critical operational reliance;
- children/consumer services;
- major changes to billing/payment processing.

## Authority notes checked 8 September 2026

- ICO: new data-protection complaints duty is in force and requires a clear complaint route, acknowledgement within 30 days, appropriate investigation, updates and outcome communication.
- ICO: SARs must normally be answered without undue delay and within one month; complex/multiple requests may be extended by up to two further months and the search must be reasonable and proportionate.
- ICO: current data-protection fee tiers start at £52 for Tier 1, with a £5 Direct Debit discount.
- ICO: controller-processor arrangements require a written contract containing the Article 28 processing details and mandatory processor terms.
- GOV.UK: a limited-company website/business letters/order forms must display registered number, registered office, jurisdiction of registration and limited-company status.
