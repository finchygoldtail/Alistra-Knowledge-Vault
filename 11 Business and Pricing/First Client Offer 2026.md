---
title: First Client Offer 2026
type: business
status: proposed-working-offer
owner: Alistair
created: 2026-09-10
updated: 2026-09-10
tags: [pricing, sales, discount, first-client, framework]
related: ["[[Client Pricing Pack]]", "[[Data Licensing and Custody Options]]", "[[13 Client Framework Agreement]]", "[[14 Client Order Form and Service Schedule]]", "[[Client Quote Template]]"]
---

# First Client Offer 2026

> **Commercial working proposal.** Figures exclude VAT and bind AlistraGIS only when written into a signed Order Form. This document defines the discounted structure for the **first paying customer** and the conditions attached to it.

## 1. The offer in one line

**10% off all recurring software fees for the first contract year**, in exchange for a signed reference and case-study rights, available to the first paying customer only.

## 2. What the discount does and does not cover

| Covered by the 10% | Not covered |
|---|---|
| Core Platform licence | Data migration and professional services |
| Optional module fees | Onboarding fee |
| Additional user seats | Customer-hosted activation fee |
| Additional project capacity | Third-party data purchased on the Customer's behalf |
| Support tier uplift | Cloud infrastructure pass-through |
| | Storage above the included allowance |

**Reason:** discounting services and pass-through costs discounts work already being paid for, or cost with no margin in it. The discount comes out of software margin, where it belongs.

## 3. How it interacts with the annual prepayment discount

The standard price book already offers **10% for annual payment in advance** ([[Client Pricing Pack]] section 11).

**These two do not stack to 20%.** The rule to state in the quote:

> The first-customer discount and the annual prepayment discount are alternatives. Where both would apply, the Customer receives the better of the two, not both. Where the Customer pays annually in advance **and** is the first customer, an additional **5%** applies for the first year only, giving **15% in total for year one**.

That gives a first customer paying annually a genuine 15% in year one, keeps the arithmetic simple, and does not set a precedent of 20% off list.

## 4. What AlistraGIS gets in return

The discount is not a giveaway. Write these into the Order Form as Special Conditions:

1. **Named reference.** The Customer agrees to act as a named reference for up to four prospect conversations or site visits per year, at reasonable notice.
2. **Case study.** The Customer agrees to a written case study, subject to its approval of the text before publication, within six months of go-live.
3. **Logo use.** Permission to use the Customer's name and logo on the AlistraGIS website and sales material, revocable on 30 days' notice.
4. **Feedback.** A structured feedback session at 30, 90 and 180 days after go-live.
5. **Minimum term.** A 12-month initial term rather than a rolling monthly arrangement.

If the Customer will not agree to reference and case-study rights, the discount should be reduced or withdrawn. That is the trade.

## 5. Discount authority

- 10% first-customer discount: **pre-approved** by this document.
- The additional 5% for annual prepayment in year one: **pre-approved** by this document.
- Anything beyond 15%: **director approval, recorded in the quote file**, per [[Client Pricing Pack]] section 13.
- Never discount third-party pass-through below cost.
- Never discount the customer-hosted activation fee — it is real engineering work.

## 6. Worked offer — Model A, we handle the data

**The recommended first-client shape.** Core Platform, QA & Audits, Operations & Production, Work Packs, 15 users, AlistraGIS-managed shared hosting, Standard Support.

### Recurring, monthly

| Line | List |
|---|---:|
| Core GIS Platform (10 users, 5 projects, 100 GB) | £1,250 |
| QA & Audits | £350 |
| Operations & Production | £450 |
| Work Packs | £350 |
| 5 additional users @ £30 | £150 |
| **Monthly recurring, list** | **£2,550** |

### Year one

| | Monthly | Annual |
|---|---:|---:|
| List recurring | £2,550 | £30,600 |
| First-customer discount only (10%) | £2,295 | £27,540 |
| **Annual prepay + first customer (15%)** | **£2,167.50** | **£26,010** |

### One-off

| Line | Price |
|---|---:|
| Standard production onboarding | £1,500 |
| Data assessment and import plan | £900 |
| Bulk design pack import — medium, if required | £3,400 |

### Headline numbers to quote

- **Year one, annual prepay, no migration:** £26,010 + £1,500 onboarding = **£27,510**
- **Year one, annual prepay, with assessment and medium migration:** **£31,810**
- **Year two onwards at list, annual prepay:** £27,540
- **Saving to the Customer in year one:** £4,590 against list

## 7. Worked offer — Model B, we handle the data, dedicated environment

Same modules and users, dedicated environment.

### Recurring, monthly

| Line | List |
|---|---:|
| Software as Model A | £2,550 |
| Dedicated environment management | £850 |
| **Monthly recurring, list** | **£3,400** |

### Year one

| | Monthly | Annual |
|---|---:|---:|
| List recurring | £3,400 | £40,800 |
| **Annual prepay + first customer (15%)** | **£2,890** | **£34,680** |

### One-off

| Line | Price |
|---|---:|
| Dedicated environment setup | £2,500 |
| Standard production onboarding | £1,500 |

- **Year one, annual prepay, no migration:** **£38,680**
- **Year two onwards at list, annual prepay:** £36,720

Note the dedicated environment surcharge is **not** discounted below the management cost in later years. Qualify hard whether isolation is genuinely required before quoting this.

## 8. Worked offer — Model C, the client handles the data

Same modules and users, customer's own Azure/AWS/PostGIS.

### Recurring, monthly

| Line | List |
|---|---:|
| Software as Model A | £2,550 |
| Customer-hosted integration and support surcharge | £450 |
| **Monthly recurring, list** | **£3,000** |

### Year one

| | Monthly | Annual |
|---|---:|---:|
| List recurring | £3,000 | £36,000 |
| **Annual prepay + first customer (15%)** | **£2,550** | **£30,600** |

### One-off — none of which is discounted

| Line | Price |
|---|---:|
| Architecture and security discovery (2 days @ £900) | £1,800 |
| Customer-hosted implementation and activation | From £4,500 |
| Standard production onboarding | £1,500 |
| **One-off subtotal** | **From £7,800** |

Plus the Customer's own cloud, database and backup costs, paid directly by the Customer.

- **Year one, annual prepay, no migration:** **From £38,400**, plus the Customer's cloud bill

### Conditions that must appear on any Model C quote

1. Priced as a **paid implementation project**, not an available configuration.
2. Discovery is completed and the fixed implementation quote agreed **before** the subscription start date.
3. Production data is not loaded until the acceptance checklist in [[15 Hosting and Data Responsibility Schedule]] section 8 passes.
4. An agreed acceptance date, with what happens if it is missed.
5. The Customer is responsible for its own infrastructure availability, backup verification and cost.

**Do not sign a Model C Order Form that reads as though the service is live on day one.** It is not, as at 10 September 2026.

## 9. Which to lead with

Lead with **Model A** and quote **£27,510 for a fully onboarded first year**.

It is live, proven, the cheapest of the three, and the fastest to a working system. If the customer raises isolation or sovereignty, present B and C with their real numbers — including the point in [[Data Licensing and Custody Options]] section 11 that **C costs more, not less**.

The three-year comparison is a strong close:

| | Model A | Model B | Model C |
|---|---:|---:|---:|
| Year one with first-customer pricing | £27,510 | £38,680 | From £38,400 + cloud |
| Three-year total | £82,590 | £112,120 | £103,200 + cloud |

## 10. Offer validity and protection

- Quote validity: **30 days** from issue.
- Applies to the **first paying customer only**; state that plainly so it is understood as a one-off, not a new list price.
- Year-two pricing reverts to list less any applicable annual prepayment discount. **Put the year-two figure in the quote** so the renewal is not a surprise.
- Any annual increase mechanism must be written into the Order Form. Do not leave it silent.
- If the Customer wants a multi-year commitment, do not automatically extend the discount — trade it against a longer non-cancellable term, per [[Client Pricing Pack]] section 11.

## 11. Checklist before issuing

- [ ] Customer legal name and company number confirmed from Companies House.
- [ ] Modules match what the licence engine can actually enforce.
- [ ] Seat count and project allowance agreed.
- [ ] Hosting model selected, and Model C flagged as an implementation project if chosen.
- [ ] Migration scope assessed, or an assessment quoted.
- [ ] Support tier agreed.
- [ ] Year-two price stated.
- [ ] Reference and case-study conditions included.
- [ ] VAT position stated.
- [ ] Framework Agreement, Order Form, Hosting Schedule and DPA attached.

## Related

- [[Client Pricing Pack]]
- [[Data Licensing and Custody Options]]
- [[Client Quote Template]]
- [[13 Client Framework Agreement]]
- [[14 Client Order Form and Service Schedule]]
