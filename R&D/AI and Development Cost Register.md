# AlistraGIS AI and Development Cost Register

> Purpose: track actual AlistraGIS development expenditure and supporting evidence in one place. This is a bookkeeping/evidence register, not a statement that every cost qualifies for R&D tax relief. Final treatment should be reviewed with the accountant or R&D adviser.

## Rules

1. Record actual invoice, subscription, credit, usage or purchase cost. Do not invent token costs for subscription-included usage.
2. Keep the supplier invoice, receipt, billing export or bank evidence.
3. Separate development/test use from live customer/business use where a service is mixed.
4. Record the Alistra workstream supported by the cost.
5. Link technical R&D expenditure to the Engineering Journal where applicable.
6. Track ordinary commercial, legal, marketing, domain and administrative costs as business costs even when they are not R&D qualifying.
7. Record VAT separately where required by the accounting records.

## Master Cost Register

| Date / period | Supplier | Product / service | Cost type | Actual cost | Currency | Development allocation | R&D allocation | Workstream / purpose | Evidence | Status / notes |
|---|---|---|---|---:|---|---:|---:|---|---|---|
| Aug 2026 | OpenAI | ChatGPT Plus | Subscription | To enter from invoice | Invoice currency | To review | To review | AlistraGIS architecture, debugging, technical design, R&D records, implementation handovers | OpenAI invoice + dated conversations | Do not estimate per-token value for subscription-included usage |
| Aug 2026 | OpenAI | Codex / flexible usage | Included usage / credits | To enter | Invoice currency | To review | To review | AlistraGIS code implementation, review, debugging and refactoring | OpenAI/Codex usage or credit receipt + GitHub commits | Separate included usage from purchased credits |
| Aug 2026 | Anthropic | Claude / Claude Code | Subscription / usage / credits | To enter from invoice | Invoice currency | To review | To review | AlistraGIS implementation, code review, refactoring, testing and architecture | Anthropic invoice/usage + GitHub commits | Record actual subscription and any extra usage separately |
| Aug 2026 | GitHub | GitHub plan / development services | Subscription | To enter from invoice | Invoice currency | To review | To review | Source control, vault, CI/development workflow | GitHub invoice/billing | Split any clearly non-development use if material |
| Aug 2026 | Vercel | Hosting / build / deployment | Subscription / usage | To enter from invoice | Invoice currency | To review | To review | Development, preview and test deployments | Vercel invoice + deployment records | Separate development/test from future live-customer hosting |
| Aug 2026 | Google / Firebase | Firebase / Google Cloud | Usage | To enter from billing export | Invoice currency | To review | To review | Auth, Firestore, Storage, Functions, test data, development | Firebase/GCP billing export | Apportion live/business use if introduced |
| Aug 2026 | Mapping provider | Map tiles / geospatial services | Subscription / usage | To enter from invoice | Invoice currency | To review | To review | GIS development and map testing | Supplier invoice/usage report | Record provider and product when invoice available |
| Aug 2026 | Domain registrar / Vercel / Cloudflare | Domains | Business cost | To enter from invoice | Invoice currency | Business allocation | Normally non-R&D / adviser review | AlistraGIS domains and brand infrastructure | Registrar invoices | Track even if not R&D qualifying |
| Aug 2026 | Email provider | Business email | Subscription | To enter from invoice | Invoice currency | Business/development allocation as appropriate | Adviser review | AlistraGIS communications / system email testing | Provider invoice | Separate general business email from technical test use where material |
| Aug 2026 | Hardware / software suppliers | Computer hardware and software | Purchase / subscription | To enter | Invoice currency | To review | Adviser review | AlistraGIS development workstation, test devices, tools | Receipts/invoices | Tax/R&D treatment to be confirmed |
| Aug 2026 | Professional advisers | Accountant / solicitor / IP / commercial advice | Professional fees | To enter | Invoice currency | Business cost | Normally outside technical R&D cost pool | Company setup, contracts, GDPR, IP, commercial advice | Adviser invoice | Track separately from technical R&D |

## AI Usage Detail

Use this table for API, purchased credits or other metered AI usage where an actual usage/cost record exists.

| Date / period | Provider | Product / model | Usage type | Input tokens | Output tokens | Other usage | Actual charged cost | Currency | Alistra workstream | Evidence |
|---|---|---|---|---:|---:|---|---:|---|---|---|
| | OpenAI | | API / credits | | | | | | | |
| | Anthropic | | API / credits | | | | | | | |

For subscription products such as ChatGPT Plus or a Claude subscription, record the subscription invoice in the Master Cost Register. Token counts may be retained as usage evidence if the provider exposes them, but do not manufacture a notional token charge where there was no separate token invoice.

## Developer Time Register

| Date / period | Person | Workstream | Activity | Actual hours | Technical R&D hours | Qualifying indirect hours | Non-R&D/product/commercial hours | Evidence | Review status |
|---|---|---|---|---:|---:|---:|---:|---|---|
| 2026-08-05 to 2026-08-07 | Alistair Grantham | Commercial GIS / spatial takeoff / API architecture | Duct/sub-duct billing model; commercial area takeoff; sundries/recipes; stock rules; package lifecycle; exports; API boundaries | To confirm | To review | To review | To review | Dated ChatGPT sessions; R&D Engineering Journal; implementation commits to follow | Reconcile actual hours before cost calculation |

## Cloud and Hosting Detail

| Period | Provider | Service | Environment | Total cost | Development/test amount | Live/business amount | Allocation method | Evidence |
|---|---|---|---|---:|---:|---:|---|---|
| | Firebase / GCP | | Dev/Test | | | | | |
| | Vercel | | Preview/Production | | | | | |
| | Mapping provider | | Dev/Test | | | | | |

## Domains, Email and Business Infrastructure

| Date | Supplier | Item | Term | Cost | Currency | Purpose | R&D treatment | Evidence |
|---|---|---|---|---:|---|---|---|---|
| | | alistragis.com | | | | Domain / brand | Track as business cost; adviser review | |
| | | alistragis.co.uk | | | | Domain / brand | Track as business cost; adviser review | |
| | | alistragis.uk | | | | Domain / brand | Track as business cost; adviser review | |

## Hardware and Test Equipment

| Date | Supplier | Item | Cost | Development use % | Business/personal use % | Workstream | Evidence | Adviser treatment |
|---|---|---|---:|---:|---:|---|---|---|
| | | | | | | | | |

## Professional and Compliance Costs

| Date | Supplier | Service | Cost | Purpose | Evidence | Accounting / R&D note |
|---|---|---|---:|---|---|---|
| | Accountant | | | Accounts / R&D review | | Track separately |
| | Solicitor | | | Contracts / licensing / IP | | Track separately |
| | Data protection / security adviser | | | GDPR / security review | | Adviser review |

## Monthly Cost Close Checklist

At each month end:

- Download OpenAI invoices and any Codex credit/usage records.
- Download Anthropic/Claude invoices and usage/credit records.
- Download GitHub invoice.
- Download Vercel invoice and usage breakdown.
- Export Firebase / Google Cloud billing.
- Download mapping provider invoice/usage.
- Add domain, email and other software subscriptions.
- Add hardware/test-device purchases.
- Add professional invoices.
- Reconcile developer hours to dated work evidence.
- Link technical costs to relevant R&D Engineering Journal entries.
- Mark uncertain R&D treatment for accountant/adviser review.
- Reconcile the register to bank/card/accounting records.

## Totals

| Category | Actual spend | Development allocation | Potential R&D amount | Evidence complete? |
|---|---:|---:|---:|---|
| AI tools | | | | No |
| Developer/director time | | | | No |
| GitHub / source control | | | | No |
| Cloud / hosting | | | | No |
| Mapping / geospatial | | | | No |
| Domains / email | | | | No |
| Hardware / software | | | | No |
| Professional fees | | | | No |
| Other | | | | No |
| **Total** | | | | |

## Important Note

This register is intended to preserve evidence and stop costs being lost. It should include all AlistraGIS-related costs, including those that ultimately do not qualify for R&D tax relief. R&D eligibility and allocation percentages should only be finalised after reviewing the relevant scheme rules and the company's actual accounting/payroll position.