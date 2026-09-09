---
title: Data Licensing and Custody Options
type: business
status: proposed-working-prices
owner: Alistair
created: 2026-09-10
updated: 2026-09-10
tags: [pricing, data, licensing, hosting, custody, framework]
related: ["[[Client Pricing Pack]]", "[[Hosting Options]]", "[[Data Ownership]]", "[[15 Hosting and Data Responsibility Schedule]]", "[[13 Client Framework Agreement]]", "[[First Client Offer 2026]]"]
---

# Data Licensing and Custody Options

> **Commercial working proposal — not a published price list.** Figures are exclusive of VAT and become binding only when written into a signed Order Form. Read alongside [[Client Pricing Pack]], which prices the software; this document prices **the data**: where it lives, who is responsible for it, what it costs to put in, take out and keep.

## 1. The question this answers

Every prospect asks a version of the same question: *"where does our network data actually sit, and who controls it?"*

There are three honest answers, and they carry different prices, different responsibilities and different levels of readiness. This document sets out all three so a quote can be built without inventing terms on a call.

**The short version for a first conversation:**

| | Who holds the data | Who pays the cloud bill | Available today |
|---|---|---|---|
| **Model A — We handle it** | AlistraGIS, shared platform | AlistraGIS | **Yes, live** |
| **Model B — We handle it, ring-fenced** | AlistraGIS, dedicated environment | AlistraGIS | **Yes, on request** |
| **Model C — You handle it** | Customer's own cloud/database | Customer | **Not yet — see section 6** |

## 2. What the customer owns, in every model

This does not change between models and should be said early, because it is the thing customers are actually worried about.

- **The Customer owns its own data.** Network records, asset data, geometry, survey and QA records, photographs, documents, production records and exports are the Customer's property.
- **AlistraGIS owns the platform.** Software, database schema, APIs, interface and documentation remain AlistraGIS's intellectual property. Nothing in a subscription transfers the software.
- **AlistraGIS takes a licence to use the data only to run the service** — to host, process, back up, support and display it, and to meet legal obligations. Not to sell, not to share, not to train third-party AI on it without a separate written agreement.
- **Aggregated, fully anonymised statistics** (volumes, performance, feature use) may be used to operate and improve the platform. This must be genuinely anonymised and stated in the Order Form. If the Customer objects, it should be capable of being switched off.
- **The Customer gets its data back on exit.** See section 8.

See [[Data Ownership]] for the full working position and [[13 Client Framework Agreement]] clauses 7 and 17.

## 3. Model A — AlistraGIS handles the data (shared platform)

The live product. Customer data sits in AlistraGIS's own Firebase/GCP environment, logically separated per company, in **europe-west2 (London)**.

### What it costs

| Item | Price |
|---|---:|
| Data custody, backup and management | **Included in Core Platform** (£1,250/month) |
| Included storage allowance | **100 GB** |
| Additional storage | **£35 per 100 GB block per month** |
| Backup and point-in-time recovery | **Included** |
| Standard annual data export | **Included, one per contract year** |
| Additional ad-hoc full export | **£450 each** |

### What the Customer gets

- Data held in the UK region, on infrastructure AlistraGIS runs and monitors.
- Backups and a proven restore procedure (see [[Stage 20 Backup Implementation]] and [[Stage 21 Restore Test]]).
- No cloud account, no database administration and no infrastructure cost of their own.
- Fastest route to being live — no provisioning work.

### What the Customer takes on

- Accepting a shared platform with logical rather than physical separation.
- Accepting AlistraGIS's subprocessors (see [[Subprocessor Register]]).

### Who to sell this to

Contractors and operators who want the software to work on Monday and have no internal cloud or DBA capability. **This should be the default recommendation, including for the first client.**

## 4. Model B — AlistraGIS handles the data (dedicated environment)

For customers whose procurement or client contracts require their data to be physically separated from other customers, but who still do not want to run it themselves.

### What it costs

| Item | Price |
|---|---:|
| Dedicated environment setup | **From £2,500 one-off** |
| Dedicated environment management | **£850 per month** |
| Included storage allowance | **250 GB** |
| Additional storage | **£30 per 100 GB block per month** |
| Dedicated backup schedule and retention | **Included** |
| Standard annual data export | **Included, one per contract year** |
| Additional ad-hoc full export | **£450 each** |

Unusually high infrastructure or egress usage may be passed through where the Order Form says so. The exact architecture and data region are quoted after technical discovery.

### Who to sell this to

Customers with a prime contractor or public-sector client imposing isolation requirements; anyone whose security questionnaire rules out multi-tenancy. It is a meaningful uplift — roughly **£10,200 a year plus setup** — so qualify whether the requirement is real or assumed before quoting it.

## 5. Model C — The Customer handles the data (customer-hosted)

The customer provides its own Azure, AWS or PostgreSQL/PostGIS environment. AlistraGIS runs the application against it. The customer's data never leaves the customer's own cloud account.

### What it costs

| Item | Price |
|---|---:|
| Implementation and activation | **From £4,500 one-off** |
| Platform integration and hosting support | **£450 per month** |
| Customer's own cloud and database costs | **Paid by the Customer, directly** |
| Architecture / security discovery | **£900 per day** |
| Complex networking, private endpoints, SSO, bespoke backup, HA/DR | **Quoted — not included** |
| Data migration into the customer environment | **£850 per day** |

### The honest position, which must be stated in writing

**This is not yet live for any customer.** The code exists — a PostgreSQL/PostGIS repository sits behind the storage router — but the router deliberately **fails closed** for Azure and AWS profiles, and no customer environment has been provisioned or accepted. Confirmed again on 10 September 2026.

That means:

- It must **not** be sold as "available now" or "a configuration setting".
- It must **not** appear on a signed Order Form as live without a dated activation plan.
- It must pass the acceptance checklist in [[15 Hosting and Data Responsibility Schedule]] section 8 before any production data is loaded.
- Quote it as **"available subject to a paid implementation project"**, with the implementation fee, the discovery day rate and an agreed acceptance date.

Selling this as ready is the single easiest way to end up in dispute with the first client. If a prospect insists on it, the correct move is a **paid discovery engagement** (2–3 days at £900/day) producing a fixed implementation quote and an acceptance date, not a subscription promise.

### Who to sell this to

Network operators and larger contractors with an existing cloud estate and a security policy requiring data to remain in their own tenant. Expect it to be asked about far more often than it is genuinely required.

## 6. Data in — getting the customer's network onto the platform

The single biggest practical obstacle to a first client is their existing data, which will arrive as KML, GeoJSON, shapefiles, spreadsheets and PDFs of varying quality.

| Service | Price |
|---|---:|
| Standard import (supported formats, customer-prepared, up to 2 datasets) | **Included in onboarding** (£1,500) |
| Data migration and transformation | **£850 per day** |
| Bulk design pack import — small (under 5,000 assets) | **£1,700 fixed (2 days)** |
| Bulk design pack import — medium (5,000–25,000 assets) | **£3,400 fixed (4 days)** |
| Bulk design pack import — large (25,000+ assets) | **Quoted after a paid data assessment** |
| Data assessment and import plan | **£900 one day, credited against the migration if it proceeds** |

**Always quote the assessment first for anything beyond a couple of clean files.** Fixed-price migration on unseen data is how a project loses money.

### Data quality assumptions to state in the Order Form

- Coordinates supplied in a documented, consistent reference system.
- One row or feature per asset, with a stable identifier.
- Duplicate, unnamed or geometry-less records are reported back, not silently invented.
- Reprocessing after the Customer supplies corrected source data is chargeable at the day rate.

## 7. Data out — exports, handover and reporting

| Service | Price |
|---|---:|
| Standard exports through the product (GeoJSON, KML, CSV, PDF, job packs) | **Included** |
| Annual full-estate export | **Included, one per contract year** |
| Additional ad-hoc full-estate export | **£450 each** |
| Bespoke export format or client-specific handover schema | **£900 per day** |
| Scheduled/automated export feed to a customer system | **From £250 per month per integration**, plus engineering |
| Export on termination | **Included once — see section 8** |

## 8. Retention, archive and exit

| Item | Price |
|---|---:|
| Retention during the term | **Included**, per [[Data Retention Schedule]] |
| Final export on termination (standard formats) | **Included, once** |
| Bespoke exit format or migration assistance | **£900 per day** |
| Post-termination archive hold | **£150 per 100 GB per month**, minimum 3 months |
| Certified deletion and written confirmation | **Included** |
| Sandbox / training copy environment | **£250 per month** |

Exit terms are a common sticking point in procurement. Being able to say *"your data comes back in open formats, once, at no charge, and we confirm deletion in writing"* is a selling point — say it early rather than defending it late.

## 9. Third-party and licensed data

AlistraGIS does not grant rights to third-party datasets it does not own.

| Data | Position |
|---|---|
| Base mapping (Esri / OpenStreetMap tiles) | Provided under the platform's own arrangements; attribution preserved in the product and on exported sheets |
| Ordnance Survey products | **Customer's own licence.** AlistraGIS does not sublicense OS data |
| Openreach PIA / duct and pole records | **Customer's own agreement with Openreach.** Held in the platform on the Customer's behalf, under the Customer's licence terms |
| Address / UPRN data | Customer's own licence unless separately agreed |
| Customer-supplied design packs | Customer's data, Customer's responsibility for its rights to supply it |

Where AlistraGIS has to procure a third-party dataset on the Customer's behalf: **at cost plus 15% administration**, stated in the Order Form.

The Customer must warrant it has the right to upload what it uploads. This is already covered in [[13 Client Framework Agreement]] clause 16 and should not be softened.

## 10. Maintenance, support and changes to the software

Confirmed figures, replacing the placeholders previously in [[Maintenance and Upgrades]].

| Item | Price |
|---|---:|
| Standard Support and platform maintenance | **Included in Core Platform** |
| Priority Support | **£500 per month** |
| Enterprise / Extended Support | **From £1,250 per month** |
| Customer-requested change or enhancement | **£900 per day** |
| Integration / API engineering | **£900 per day** |
| Out-of-scope engineering | **£150 per hour**, minimum 2 hours |
| Agreed out-of-hours emergency work | **£250 per hour**, minimum 2 hours, by prior written agreement only |

### What "maintenance" includes at no extra charge

- Security patches and dependency updates.
- Defect correction in delivered functionality.
- Platform updates and improvements released to all customers.
- Backup operation and monitoring.
- Ordinary account, licence and permission support.

### What it does not include

- New features specific to one customer.
- Integrations with the customer's other systems.
- Data correction caused by customer-supplied data.
- Training beyond the onboarding allowance.
- Anything the Order Form lists as excluded.

**Do not promise a roadmap item as a contractual deliverable in an Order Form.** If a customer needs a specific capability by a specific date, that is chargeable development with an agreed acceptance test, not a subscription inclusion.

## 11. Model comparison — three-year cost of ownership

Assumes Core Platform plus QA & Audits, Operations & Production and Work Packs, 15 users, standard support, annual prepayment at the standard 10% annual-prepay discount. Excludes VAT, migration and the Customer's own cloud costs.

| | Model A (we hold it) | Model B (we hold it, dedicated) | Model C (client holds it) |
|---|---:|---:|---:|
| Recurring per month, list | £2,550 | £3,400 | £3,000 |
| Year 1 recurring after annual prepay discount | £27,540 | £36,720 | £32,400 |
| One-off setup / activation | £1,500 | £4,000 | £6,000 |
| *Model C excludes discovery* | — | — | *add £1,800 for 2 days* |
| **Year 1 total** | **£29,040** | **£40,720** | **£38,400** |
| Years 2 and 3 each | £27,540 | £36,720 | £32,400 |
| **Three-year total** | **£84,120** | **£114,160** | **£103,200** |
| Plus the Customer's own cloud bill | — | — | **Yes, on top** |

The point to make in a sales conversation: **Model C is not the cheap option.** It costs more with AlistraGIS *and* adds the customer's own infrastructure bill and internal administration. It buys control, not savings. Customers frequently assume the opposite.

## 12. What to put in front of the first client

1. Lead with **Model A**. It is live, proven, cheapest, and fastest to value.
2. Have **Model B** ready as the answer to an isolation requirement.
3. Present **Model C** honestly as a paid implementation project with a discovery phase — never as a switch.
4. Quote data migration after a paid assessment, not before.
5. State the exit terms unprompted. It removes the biggest objection in the room.

See [[First Client Offer 2026]] for the discounted first-customer structure.

## 13. Before this is used commercially

- [ ] Validate the 100 GB and 250 GB allowances against actual Firebase/GCP cost behaviour and set a billing alert.
- [ ] Confirm the storage overage rates cover real cost plus margin.
- [ ] Accountant to confirm VAT treatment of pass-through infrastructure and third-party data.
- [ ] Solicitor to confirm the data-ownership, AI/anonymised-statistics and exit wording in the Framework Agreement matches this document.
- [ ] Do not quote Model C as live until the acceptance checklist passes.

## Related

- [[Client Pricing Pack]]
- [[Hosting Options]]
- [[Data Ownership]]
- [[First Client Offer 2026]]
- [[15 Hosting and Data Responsibility Schedule]]
- [[Data Retention Schedule]]
