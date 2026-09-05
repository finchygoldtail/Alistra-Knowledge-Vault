---
title: API Buyout
type: business
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-09-05
tags: [api, pricing]
---

# API Buyout

## What "the API" actually is

Every Cloud Functions callable in `functions/src/` (map assets, licence, storage profile, production, QA, FAS import, work packs, employees, tickets, commercial packages, and more) is authenticated via Firebase Auth tokens and gated by company + role on every call — there is no unauthenticated or anonymous API surface today. "Buying the API" means one of two genuinely different things, and a buyer should be told clearly which one is on offer:

1. **API access as part of the product** — a customer's own systems calling AlistraGIS's hosted API to read/write their own company's data (e.g. pushing production updates from another system). Technically straightforward: it's the same callables the frontend already uses, just called by something other than the AlistraGIS UI. Needs an API key/service-account story that doesn't exist yet (today, every caller is a signed-in human user via the Firebase Auth flow) — that's a real gap to scope, not just a pricing one.
2. **Source code / IP buyout** — selling rights to the backend source itself. This is an intellectual-property and licensing question, not a hosting one — see [[Intellectual Property]] and [[Licensing Options]]. Needs an actual solicitor's involvement before it's offered; nothing here should be read as a substitute for that.

## What needs deciding before this is sellable

- Whether (1) is even wanted as a product — a machine-to-machine auth path (service accounts / API keys with company + role scoping) doesn't exist in the code yet.
- If (2) is ever on the table: what's licensed (source access vs. a white-label deployment vs. full IP transfer), and under what restrictions (no resale, no rebrand, exclusivity terms, ongoing support obligations).

Pricing for either can't be set responsibly until the scope above is actually decided — this page is deliberately not proposing figures, unlike the other pages in this folder, because the *product* isn't defined yet, not just the price.

## Related

- [[API Catalogue]] — the technical API documentation this commercial decision would need to match.
- [[Licensing Options]]
- [[Intellectual Property]]
