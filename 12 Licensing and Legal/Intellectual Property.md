---
title: Intellectual Property
type: legal
status: draft-for-solicitor-review
owner: Alistair
created: 2026-08-02
updated: 2026-09-10
tags: [legal, ip, licensing, brand]
related: ["[[Data Ownership]]", "[[13 Client Framework Agreement]]", "[[02 Software and SaaS Licence Agreement]]", "[[API Buyout]]", "[[10 Third Party Licence Register]]"]
---

# Intellectual Property

> **Draft for UK technology solicitor review.** Sets out the working position AlistraGIS intends to take. Confirm against the executed Framework Agreement before relying on it with a customer.

The companion to [[Data Ownership]]: that document covers the **data**, this one covers the **software and everything around it**.

## 1. What AlistraGIS owns

All of the following are AlistraGIS's property and no subscription transfers any of it:

- **Source code** — the application, Cloud Functions, database schema, security rules, build tooling and scripts.
- **APIs** — design, structure, endpoints, contracts and documentation.
- **User interface** — layout, design system, navigation, iconography and interaction design.
- **Documentation** — user guides, technical documentation, onboarding material and training content.
- **Templates and layouts** — job sheets, job packs, as-built drawing layouts, report and export formats, workbook structures.
- **Data model** — asset classification, naming conventions, the network model, the production and work-pack model.
- **Brand** — the AlistraGIS and Alistra names, logos, domains and get-up. See [[14 Intellectual Property and Brand Protection]].
- **Improvements** — any enhancement to the platform, however it arose, including from customer suggestions.

## 2. What the customer gets

A **non-exclusive, non-transferable, revocable licence to use** the platform for its own internal business purposes for the term, limited to the modules, users and projects on the Order Form.

The customer may **not**:

- copy, decompile, reverse-engineer or attempt to derive the source code;
- resell, sublicense, rent or provide the platform as a service to a third party;
- use it to build a competing product;
- remove or obscure proprietary notices or attribution;
- give access to a competitor of AlistraGIS;
- exceed the licensed user, module or project entitlement.

Sharing named accounts between people is a licence breach, not a grey area. Say so in the Order Form.

## 3. Customer suggestions and feedback

If a customer suggests an improvement and AlistraGIS builds it, **AlistraGIS owns it**, and may make it available to every other customer.

This must be stated explicitly. Without it, a customer who asked for a feature can later claim a share in it. The customer keeps a licence to use it like any other functionality; it does not become theirs.

## 4. Bespoke development paid for by a customer

The default: **AlistraGIS owns bespoke work**, and the customer receives a licence to use it.

Reasons to hold that line:

- The work is built on AlistraGIS's platform and cannot meaningfully be separated from it.
- Fragmenting ownership across customers makes the codebase unmaintainable.
- The day rate is priced as development, not as a transfer of intellectual property.

Where a customer insists on owning bespoke work, the options in order of preference:

1. **Exclusivity period** — AlistraGIS owns it, but will not offer it to a named competitor for an agreed period. Usually settles it.
2. **Priced assignment** — ownership transfers at a materially higher price reflecting the loss of reuse, with a licence back to AlistraGIS.
3. **Refuse.** Some requests are not worth taking.

Never agree to assign ownership of anything that touches the core platform.

## 5. Third-party components

The platform uses open-source and third-party components. Their licences are recorded in [[10 Third Party Licence Register]] and the notices in [[11 THIRD_PARTY_NOTICES]].

- AlistraGIS is responsible for complying with those licences.
- Attribution required by a licence must be preserved in the product and on exported material.
- Base mapping attribution appears in the product and on generated job sheets — this is a licence obligation, not decoration, and must not be removed to tidy a layout.
- Adding a new dependency means checking its licence **before** it ships. A copyleft licence in the wrong place is a serious problem to unwind later.

## 6. Source code escrow

Larger customers, particularly public-sector or prime contractors, may ask what happens to their operation if AlistraGIS ceases to trade.

Options, cheapest first:

1. **Contractual exit assistance and a full data export.** Usually enough, and already offered — see [[Data Ownership]] section 8.
2. **Escrow of a data export**, held by a third party.
3. **Full source-code escrow** with a recognised agent, released on defined events.

Full escrow costs real money annually and needs the release conditions drafted carefully. **Price it as a chargeable option, do not include it as standard,** and do not agree to it verbally in a sales meeting.

## 7. The API question

[[API Buyout]] covers two genuinely different things that must never be conflated:

- **Hosted API access** — the customer integrates its own systems with the platform. A licence to use, priced per integration. This is ordinary.
- **A source or IP licence to the API itself** — the customer takes the code. This is a company-level decision with valuation implications, not a sales decision, and should not be discussed as though it were a pricing option.

## 8. Brand and trade marks

- The AlistraGIS name, logo and get-up are AlistraGIS's. Customers get no right to use them beyond identifying the platform they use.
- Customer logo and name use by AlistraGIS requires the customer's permission — which is exactly what the first-client offer trades for a discount. See [[First Client Offer 2026]].
- Trade mark filing status and brand protection are tracked in [[14 Intellectual Property and Brand Protection]].

## 9. Infringement and indemnity

The working position, subject to solicitor review:

- AlistraGIS warrants that the platform, used as permitted, does not knowingly infringe a third party's intellectual property.
- AlistraGIS will defend a claim that the platform infringes, provided the customer notifies promptly and lets AlistraGIS conduct the defence.
- That indemnity does not cover: customer data, third-party data the customer supplied, unauthorised modification, or use outside the licence.
- The customer indemnifies AlistraGIS against a claim that data it uploaded infringed someone's rights.
- Both sides' liability is subject to the caps in [[13 Client Framework Agreement]] clause 20.

**Check the indemnity against the insurance policy before signing anything.** An indemnity wider than the cover is an uninsured liability.

## 10. Still to decide

- [ ] Solicitor to confirm the ownership, feedback and bespoke-work positions survive review.
- [ ] Confirm the infringement indemnity aligns with the professional indemnity cover actually held.
- [ ] Decide the standard exclusivity period offered in place of assignment (12 months is a reasonable opening).
- [ ] Price the escrow option, or decide to decline it.
- [ ] Confirm trade mark filing status before publishing brand claims.
- [ ] Confirm every third-party licence in the register permits commercial SaaS distribution.

## Related

- [[Data Ownership]]
- [[13 Client Framework Agreement]]
- [[02 Software and SaaS Licence Agreement]]
- [[API Buyout]]
- [[10 Third Party Licence Register]]
- [[14 Intellectual Property and Brand Protection]]
- [[First Client Offer 2026]]
