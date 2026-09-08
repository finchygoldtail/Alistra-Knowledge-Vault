---
title: AlistraGIS Client Pricing Pack
type: business
status: proposed-working-prices
owner: Alistair
created: 2026-09-08
updated: 2026-09-08
tags: [pricing, licensing, modules, hosting, seats, framework]
related: ["[[Pricing Models]]", "[[Hosting Options]]", "[[13 Client Framework Agreement]]", "[[14 Client Order Form and Service Schedule]]", "[[15 Hosting and Data Responsibility Schedule]]"]
---

# AlistraGIS Client Pricing Pack

> **Commercial working proposal — not yet a published price list.** These figures are designed to give AlistraGIS a consistent quoting framework. Final prices remain a commercial decision and only become binding when included in a signed quotation/Order Form. Prices below are **exclusive of VAT**.

## 1. Pricing principles

Every customer quote is built from six variables:

1. **Core platform licence**;
2. **modules required**;
3. **number of authorised users/seats**;
4. **number of active projects/areas where applicable**;
5. **hosting model**; and
6. **implementation/support/usage requirements**.

This matches the current licence architecture, which already supports plan type, `maxUsers`, `maxProjects` and independent `enabledFeatures`.

## 2. Trial and pilot

### Standard trial

- **7 days**;
- no licence fee;
- intended for demonstration/test data rather than sensitive live production data;
- small user/project allowance configured for evaluation;
- no bespoke integration, migration or production SLA;
- expires automatically unless converted to a paid Order.

### Controlled commercial pilot

For customers needing live or customer-specific data, migration or a longer evaluation period:

- from **£2,500 one-off** for a defined 30-day pilot;
- scope, users, data, modules and hosting agreed in a Pilot Order;
- up to **£2,500 pilot fee may be credited against first-year subscription fees** if the customer converts within 30 days of pilot completion, where agreed in writing;
- production/security/DPA checks must be completed before live personal/customer-sensitive data is loaded.

## 3. Core platform licence

### Core GIS Platform — £1,250 per month

Includes:

- AlistraGIS tenant/company environment;
- Core GIS/Map, Overview and Assets capability (`map`, `overview`, `assets`);
- up to **10 active users**;
- up to **5 active projects/areas**;
- standard AlistraGIS-managed shared hosting;
- Standard Support;
- normal platform updates/security fixes;
- standard backup/recovery controls applicable to Supplier-managed hosting;
- admin/licence controls.

This is the minimum standard paid production subscription unless a bespoke Enterprise Order states otherwise.

## 4. Optional module pricing

| Module | Current feature flag / packaging | Monthly price |
|---|---|---:|
| QA & Audits | `audits` | **£350** |
| Reports & Handover Reporting | `reports` | **£250** |
| Commercial | `commercial` | **£550** |
| Operations & Production | `operations` | **£450** |
| Work Packs | `workpacks` | **£350** |
| Health & Safety / HANDS | `hands` | **£300** |

### Full current module bundle

Core Platform plus all six optional modules above:

- list price: **£3,500 per month before additional seats/hosting/support**;
- no separate bundle discount is assumed unless approved in the quote.

### Features not yet independently licence-gated

Maintenance, PIA/Permits, advanced Topology, Management APIs, FRIDAY AI and future utility-sector modules must be priced under the closest enforceable module or as a bespoke/Enterprise add-on until they have dedicated licence flags.

Do not sell a separate software entitlement that the current licence system cannot enforce unless the Order Form clearly explains the packaging.

## 5. User / seat pricing

The Core Platform includes the first **10 active customer users**.

For larger customers, use the rate corresponding to the customer's total contracted seat band for seats above the included 10:

| Total contracted users | Charge for each user above first 10 |
|---|---:|
| 11–25 | **£30/user/month** |
| 26–50 | **£25/user/month** |
| 51–100 | **£20/user/month** |
| 101–250 | **£15/user/month** |
| 251+ | **Enterprise quote** |

Supplier SuperAdmin/platform-support accounts excluded by the product's seat logic are not customer-billable seats.

### Example

A 40-user customer pays for 30 additional seats at the 26–50 band:

`30 × £25 = £750/month` additional seat charge.

## 6. Project / area capacity

Core Platform includes **5 active projects/areas**.

Working price for additional active project capacity:

- **£75 per additional active project/month**; or
- Enterprise project allowance quoted for large regional/national deployments.

Archived/read-only project treatment should be agreed before enforcing project billing so customers are not charged merely for historical data retention.

## 7. Hosting options

### A. AlistraGIS-managed shared hosting

**Included in Core Platform price** subject to normal/fair-use storage and platform limits stated in the Order Form.

Working included storage allowance:

- **100 GB** pooled customer storage;
- additional storage sold in **100 GB blocks at £35/month**;
- exceptional data-transfer/egress or third-party charges may be quoted separately where they become material.

Before this is published, verify actual Firebase/GCP/Vercel cost behaviour and set an alert threshold so the commercial allowance cannot create uncontrolled infrastructure exposure.

### B. AlistraGIS-managed dedicated environment/data layer

For customers requiring dedicated infrastructure/isolation:

- **setup from £2,500 one-off**;
- **£850/month** dedicated-environment management surcharge;
- underlying unusually high infrastructure/egress usage may be passed through where stated in the Order Form;
- exact architecture and data region quoted before contract.

### C. Customer-selected/customer-hosted Azure, AWS, PostgreSQL/PostGIS or approved server

Because customer-hosted production activation still requires customer-specific provisioning and technical validation:

- **implementation/activation from £4,500 one-off**;
- **£450/month** platform integration/hosting-support surcharge;
- Customer pays its own cloud/server/database costs directly unless otherwise agreed;
- complex networking, private endpoints, SSO, bespoke backup, HA/DR or migration are chargeable professional services;
- final price only after technical discovery.

The customer-hosted option must not be sold as live until the acceptance checklist in [[15 Hosting and Data Responsibility Schedule]] passes.

## 8. Support tiers

### Standard Support — Included

Intended for ordinary production use during standard business support hours.

Includes:

- support ticket/email intake;
- security and defect triage;
- standard product updates;
- ordinary account/licence support.

Exact response targets are controlled by the SLA.

### Priority Support — £500/month

For customers requiring named commercial/technical escalation and faster target response.

May include:

- named support contact;
- priority queue;
- scheduled service review;
- faster response targets as stated in SLA.

### Enterprise / Extended Support — from £1,250/month

For enhanced hours, operational escalation, dedicated review meetings or bespoke SLA requirements.

24/7 support, on-call engineering or guaranteed resolution must not be offered unless separately costed and operationally staffed.

## 9. Onboarding and professional services

| Service | Working price |
|---|---:|
| Standard production onboarding | **£1,500 one-off** |
| Additional remote training | **£650/day** |
| On-site training / workshop | **£750/day + reasonable travel** |
| Data migration / transformation | **£850/day** |
| Integration/API engineering | **£900/day** |
| Bespoke software development | **£900/day** |
| Architecture/security/customer-hosted discovery | **£900/day** |
| Emergency/out-of-scope engineering | **£150/hour**, minimum 2 hours, only where agreed |

### Standard onboarding includes

- tenant/company setup;
- licence/module configuration;
- initial role/permission workshop;
- up to two remote onboarding sessions;
- basic user-import template assistance;
- go-live checklist.

Large data migration, custom integrations and bespoke workflow changes are excluded unless quoted.

## 10. API and AI pricing

### API access

Where API capability is included within a customer's licensed modules, normal API use may be included subject to rate limits.

For dedicated external integration/API entitlement:

- **from £250/month per integration/application**;
- engineering/setup charged separately;
- high-volume usage may require a usage schedule.

### FRIDAY AI / third-party AI

Do not include unlimited third-party AI usage in the ordinary subscription.

Working commercial structure:

- module/access fee from **£300/month** where enabled; plus
- included usage allowance stated in Order Form; then
- pass-through or metered usage above allowance.

Provider DPA, region, security and production-readiness checks must be complete before customer personal/sensitive data is sent to the AI provider.

## 11. Billing options

### Monthly

- standard list price;
- payable monthly in advance unless Order Form says otherwise.

### Annual in advance

Working incentive:

- **10% discount** on recurring software/module/seat fees;
- hosting pass-through, professional services, usage/overage and one-off fees excluded unless specifically discounted.

### Multi-year

Do not automatically discount 2–3 year contracts. A commercial discount may be approved in exchange for:

- longer non-cancellable commitment;
- annual prepayment;
- minimum seat/module commitment;
- reference/case-study rights where appropriate;
- reduced implementation complexity.

Any multi-year price increase mechanism must be written into the Order Form.

## 12. Example quotes

### Example A — Small contractor / focused deployment

Requirements:

- Core GIS Platform;
- QA & Audits;
- Operations & Production;
- Work Packs;
- 15 users;
- AlistraGIS-managed shared hosting;
- Standard Support.

Monthly:

- Core: £1,250
- QA & Audits: £350
- Operations: £450
- Work Packs: £350
- 5 additional users × £30: £150

**Total recurring: £2,550/month excl. VAT**

Standard onboarding: **£1,500 one-off**

Annual prepay recurring after 10% discount: **£27,540/year excl. VAT**

First year incl. onboarding: **£29,040 excl. VAT**

### Example B — 50-user full operational customer

Requirements:

- Core platform;
- all six optional current modules;
- 50 users;
- shared hosting;
- Standard Support.

Monthly:

- Full current module bundle incl. core: £3,500
- 40 additional users × £25: £1,000

**Total recurring: £4,500/month excl. VAT**

Annual prepay after 10% discount: **£48,600/year excl. VAT**

Onboarding/migration quoted separately.

### Example C — 100-user full suite + customer-hosted cloud

Requirements:

- full current module bundle;
- 100 users;
- customer-selected approved Azure/AWS/PostGIS environment;
- Priority Support.

Monthly:

- Full module bundle: £3,500
- 90 additional users × £20: £1,800
- Customer-hosted integration/support surcharge: £450
- Priority Support: £500

**Recurring: £6,250/month excl. VAT**

Plus:

- customer-hosted activation from £4,500 one-off;
- customer pays its own cloud infrastructure;
- migration/integration engineering as required.

## 13. Discount authority / quote protection

Until a formal sales approval process exists:

- discounts above **10%** should require director approval and be recorded in the quote file;
- do not discount third-party pass-through costs below cost;
- do not waive customer-hosted activation work without a written reason;
- avoid perpetual fixed pricing without an explicit commercial reason;
- never promise unlimited users, storage, support or API/AI usage unless priced as Enterprise and technically protected.

## 14. Quote calculation formula

Use:

`Recurring Monthly = Core + Selected Modules + Additional Seats + Additional Projects + Hosting Surcharge + Support Upgrade + API/AI Fixed Fees`

Then add:

`One-Off = Onboarding + Migration + Training + Hosting Activation + Bespoke Development`

Annual prepay discount applies only to approved recurring software/module/seat items unless the quote explicitly states otherwise.

## 15. Required quote fields

Every client quote should state:

- quote reference/version/date;
- customer legal name;
- modules;
- users/seats;
- project allowance;
- hosting model and who pays cloud costs;
- support tier;
- recurring fees;
- one-off fees;
- usage/overage limits;
- billing frequency;
- VAT treatment;
- term and renewal;
- price validity;
- implementation assumptions;
- dependencies/technical caveats;
- Framework Agreement/Order Form references.

## 16. Commercial review before publication

Before issuing this as a public price list:

- [ ] validate hosting/storage allowances against actual cost data;
- [ ] confirm target gross margin;
- [ ] compare against at least 5 GIS/field-operations SaaS competitors where reasonably comparable;
- [ ] define standard support hours/response targets;
- [ ] decide whether public pricing or quote-only pricing is preferred;
- [ ] accountant reviews VAT/invoicing treatment;
- [ ] solicitor confirms pricing/renewal/overage wording;
- [ ] confirm customer-hosted engineering is production-ready before marketing it as generally available.

## 17. Recommended sales positioning

Sell AlistraGIS as a configurable infrastructure operations platform rather than a cheap per-user mapping tool. The value proposition is the combination of GIS, design/asset data, operational production, QA, work packs, commercial control and governance in one environment.

The modular structure allows smaller clients to start with Core + selected operational modules while larger clients can move toward full-suite Enterprise use without needing a separate product.
