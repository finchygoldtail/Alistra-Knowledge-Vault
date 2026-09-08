---
title: AlistraGIS Client Order Form and Service Schedule
status: commercial-draft-for-solicitor-review
updated: 2026-09-08
owner: Alistair
related: ["[[13 Client Framework Agreement]]", "[[15 Hosting and Data Responsibility Schedule]]", "[[Client Pricing Pack]]", "[[03 Service Level Agreement]]", "[[DPA Requirements]]"]
---

# AlistraGIS Client Order Form and Service Schedule

> Use one signed Order Form for each customer subscription or material service order. This schedule is intended to avoid rewriting the Framework Agreement for every client.

## A. Customer and Order details

| Field | Details |
|---|---|
| Order reference | [ORDER ID] |
| Customer legal name | [CUSTOMER LEGAL NAME] |
| Company number | [IF APPLICABLE] |
| Registered address | [ADDRESS] |
| Primary commercial contact | [NAME / EMAIL] |
| Technical contact | [NAME / EMAIL] |
| Privacy / DPA contact | [NAME / EMAIL] |
| Billing contact | [NAME / EMAIL] |
| Supplier | Alistra GIS Ltd trading as AlistraGIS |
| Supplier company number | 17361925 |
| Effective date | [DATE] |
| Initial term | [12 / 24 / 36 MONTHS / OTHER] |
| Renewal | [AUTO-RENEW / MANUAL RENEWAL / OTHER] |
| Billing frequency | [MONTHLY / ANNUAL IN ADVANCE / OTHER] |
| Payment terms | [e.g. 14 or 30 DAYS — SOLICITOR/COMMERCIAL APPROVAL] |
| Quote validity | [30 DAYS unless otherwise stated] |

## B. Plan and capacity

| Item | Contracted value |
|---|---:|
| Licence type | [Subscription / Enterprise] |
| Authorised users / seats | [NUMBER] |
| Included active projects | [NUMBER] |
| Additional project capacity | [NUMBER / N/A] |
| Production environment | [YES/NO] |
| Test/training environment | [YES/NO] |
| API access | [YES/NO + LIMITS] |
| AI/FRIDAY access | [YES/NO + PROVIDER/USAGE TERMS] |

Active Supplier SuperAdmin/platform-support accounts used to administer the customer tenant are not customer billable seats where the licence engine excludes them.

## C. Licensed modules

Only modules marked **Included** are licensed under this Order.

| Customer-facing module | Current licence capability / flag | Included? | Monthly fee | Notes / limits |
|---|---|---|---:|---|
| Core GIS, Map & Overview | `map`, `overview`, `assets` | [ ] | £[ ] | Core map, asset and overview capability |
| QA & Audits | `audits` | [ ] | £[ ] | Audit / QA workflows |
| Reports & Handover Reporting | `reports` | [ ] | £[ ] | Reporting/export capability as configured |
| Commercial | `commercial` | [ ] | £[ ] | Allocation, valuation, billing/commercial workflows as contracted |
| Operations & Production | `operations` | [ ] | £[ ] | Production and operational workflows |
| Work Packs | `workpacks` | [ ] | £[ ] | Work-pack/job-pack capability |
| Health & Safety / HANDS | `hands` | [ ] | £[ ] | H&S capability available under current licence flag |
| Additional / bespoke module | [FLAG / FEATURE] | [ ] | £[ ] | Must be technically supported before sale |

### Module packaging note

Some customer-facing features such as Maintenance, PIA/Permits, Management, advanced Topology, API services or future sector-specific modules may currently sit within broader technical flags or require a dedicated feature gate. Where a feature is not independently enforceable by the licence engine, the Order Form must say which licensed module contains it rather than implying a separate technical entitlement that does not yet exist.

## D. Hosting selection

Select one:

- [ ] **AlistraGIS-managed shared hosting** — standard production-supported model.
- [ ] **AlistraGIS-managed dedicated environment/data layer** — subject to separate technical scope and fee.
- [ ] **Customer-selected/customer-hosted Azure** — only when provisioned and technically approved.
- [ ] **Customer-selected/customer-hosted AWS** — only when provisioned and technically approved.
- [ ] **Customer-selected PostgreSQL/PostGIS or other approved server** — subject to supported architecture and engineering validation.

### Hosting details

| Field | Contracted value |
|---|---|
| Data-plane owner | [ALISTRAGIS / CUSTOMER] |
| Cloud/provider | [Firebase/GCP / Azure / AWS / PostgreSQL/PostGIS / Other] |
| Region(s) | [VERIFIED REGION] |
| Production database | [DETAILS / MANAGED SERVICE NAME] |
| File/object storage | [DETAILS] |
| Backup owner | [ALISTRAGIS / CUSTOMER / SHARED] |
| Backup policy | [REFERENCE / PERIOD] |
| Recovery responsibility | [REFERENCE SLA/HOSTING SCHEDULE] |
| Infrastructure charges paid by | [ALISTRAGIS / CUSTOMER] |
| Customer admin access | [DETAILS] |
| Supplier support access | [DETAILS] |
| Exit/export method | [DETAILS] |

This section must be read with [[15 Hosting and Data Responsibility Schedule]].

## E. Data protection and security

| Item | Position |
|---|---|
| Customer role for Customer Data | [Controller / Processor / Other — confirm] |
| AlistraGIS role | [Processor for Customer Data; controller for own admin/support etc. — confirm] |
| DPA required | [YES/NO] |
| DPA version | [VERSION / DATE] |
| Approved subprocessor list | [REFERENCE] |
| International transfer position | [REFERENCE / N/A] |
| Special-category data expected? | [NO unless expressly assessed and approved] |
| Criminal-offence data expected? | [NO unless expressly assessed and approved] |
| DPIA/customer privacy review required? | [YES/NO] |
| Security contact | [EMAIL] |
| Privacy contact | [EMAIL] |

## F. Implementation and onboarding

| Service | Included quantity | Fee | Notes |
|---|---:|---:|---|
| Standard tenant setup | [ ] | £[ ] | Company/tenant configuration |
| Module/licence configuration | [ ] | £[ ] | Enabled modules, seat and project limits |
| Permissions workshop | [ ] | £[ ] | Roles and access model |
| User import | [ ] users | £[ ] | Template required |
| Project/data import | [ ] | £[ ] | Subject to data-quality review |
| Branding | [ ] | £[ ] | Customer logo/branding scope |
| Training | [ ] days/sessions | £[ ] | Remote/on-site as quoted |
| Migration | [ ] days | £[ ] | Existing GIS/data migration |
| API/integration setup | [ ] | £[ ] | Defined endpoints/systems only |
| Customer-hosted provisioning | [ ] | £[ ] | Only if selected in section D |
| Bespoke development | [ ] days | £[ ] | Change-controlled |

## G. Support level

Select one:

- [ ] **Standard Support** — included in base subscription unless stated otherwise.
- [ ] **Priority Support** — enhanced commercial support fee applies.
- [ ] **Enterprise / Extended Support** — bespoke SLA/service hours.

SLA version: [VERSION / DATE]

Support hours: [DETAILS]

Named contacts/escalation: [DETAILS]

## H. Commercial summary

| Charge | Monthly | One-off |
|---|---:|---:|
| Base platform / Core GIS | £[ ] | — |
| Module fees | £[ ] | — |
| User/seat fees | £[ ] | — |
| Project-capacity fees | £[ ] | — |
| Hosting/environment fee | £[ ] | £[ ] |
| Support upgrade | £[ ] | — |
| API/AI/usage allowance | £[ ] | — |
| Implementation/onboarding | — | £[ ] |
| Migration/training | — | £[ ] |
| Bespoke development | £[ ] / as used | £[ ] |
| **Subtotal excl. VAT** | **£[ ]** | **£[ ]** |
| VAT | £[ ] | £[ ] |
| **Total** | **£[ ]** | **£[ ]** |

Annual prepayment discount, if any: [ ]%

First-year annual contract value (excl. VAT): **£[ ]**

## I. Usage and overages

Where applicable, record agreed included limits and overage rates:

| Metric | Included | Overage / additional price |
|---|---:|---:|
| Storage | [ ] GB | £[ ] |
| Data transfer/egress | [ ] | £[ ] |
| API calls | [ ] | £[ ] |
| AI usage | [ ] | £[ ] / pass-through |
| Additional user | [ ] | £[ ] per user/month |
| Additional active project | [ ] | £[ ] per project/month |
| Additional support/professional time | [ ] | £[ ] per day/hour |

No usage charge should be applied unless the metric and charging method are stated here or agreed through a Change Order.

## J. Special Conditions

[INSERT NEGOTIATED CUSTOMER-SPECIFIC TERMS. DO NOT ALTER THE MASTER FRAMEWORK INFORMALLY BY EMAIL.]

## K. Dependencies / assumptions

- Customer provides accurate source data in agreed format.
- Customer appoints authorised commercial, technical and privacy contacts.
- Customer-hosted options are conditional on technical validation and supported versions.
- Data residency statements are conditional on live provider/account verification.
- Safety-critical and physical works require independent statutory, survey, engineering and safe-working verification.
- Roadmap/demo functionality is excluded unless specifically listed in this Order.

## L. Documents incorporated

- [[13 Client Framework Agreement]]
- [[15 Hosting and Data Responsibility Schedule]]
- [[02 Software and SaaS Licence Agreement]]
- [[01 Standard Terms and Conditions]]
- [[03 Service Level Agreement]]
- signed Data Processing Agreement where required
- applicable Privacy/Security/Subprocessor documentation

## M. Signatures

By signing, each Party confirms that the authorised signatory has authority to bind that Party and that the Order incorporates the documents listed above.

### Alistra GIS Ltd

Name: ______________________________  
Title: _______________________________  
Signature: ___________________________  
Date: _______________________________

### Customer

Legal name: __________________________  
Name: ______________________________  
Title: _______________________________  
Signature: ___________________________  
Date: _______________________________
