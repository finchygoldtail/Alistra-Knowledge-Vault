---
title: Maintenance and Upgrades
type: business
status: proposed-working-prices
owner: Alistair
created: 2026-08-02
updated: 2026-09-10
tags: [maintenance, pricing, support, changes]
related: ["[[03 Service Level Agreement]]", "[[Client Pricing Pack]]", "[[Data Licensing and Custody Options]]", "[[Module and Seat Ready Reckoner]]"]
---

# Maintenance and Upgrades

> Figures exclude VAT and bind AlistraGIS only when written into a signed Order Form. Committed response times live in [[03 Service Level Agreement]] — this page must agree with it, never contradict it.

## 1. What maintenance actually covers

Included in every paid subscription, at no extra charge:

- **Security patches and dependency updates.**
- **Defect correction** in functionality already delivered.
- **Platform updates and improvements** released to all customers.
- **Backup operation, monitoring and restore capability.**
- **Ordinary account, licence, role and permission support.**
- **Compatibility maintenance** as browsers and devices move.

Not included, and chargeable:

- New features specific to one customer.
- Integrations with the customer's other systems.
- Data correction arising from customer-supplied data.
- Training beyond the onboarding allowance.
- Anything the Order Form lists as excluded.

## 2. Support tiers and prices

Confirmed figures, consistent with [[Client Pricing Pack]] section 8.

| Tier | Bug fixes | Influence on roadmap | Response | Price |
|---|---|---|---|---:|
| **Standard** | Included, triaged by severity | Roadmap-driven, not guaranteed | Business hours | **Included in Core** |
| **Priority** | Included, prioritised | Some influence, scheduled review | Same business-day acknowledgement | **£500/month** |
| **Enterprise / Extended** | Included, prioritised | Negotiated custom work | Named contact, bespoke SLA | **From £1,250/month** |

**Do not offer 24/7 support, on-call engineering or guaranteed resolution times** unless separately costed and actually staffed. There is currently one person. An SLA that cannot be met is worse than no SLA.

## 3. Chargeable work — changes to the program

This is the section customers ask about once they are live and want something changed.

| Work | Rate |
|---|---:|
| Customer-requested change or enhancement | **£900 per day** |
| Integration / API engineering | **£900 per day** |
| Bespoke software development | **£900 per day** |
| Architecture / security / customer-hosted discovery | **£900 per day** |
| Data migration and transformation | **£850 per day** |
| Remote training | **£650 per day** |
| On-site training or workshop | **£750 per day** plus reasonable travel |
| Out-of-scope engineering | **£150 per hour**, minimum 2 hours |
| Agreed out-of-hours emergency work | **£250 per hour**, minimum 2 hours, by prior written agreement only |

### How a change request should run

1. Customer raises the request in writing.
2. AlistraGIS provides a **written estimate in days**, with assumptions and what is excluded.
3. Customer approves in writing before work starts.
4. Work is delivered and demonstrated against an agreed acceptance test.
5. Invoiced on acceptance, or monthly in arrears for work over five days.

**Never start chargeable work on a verbal request.** A change nobody approved is a change nobody pays for.

### Small changes

A change under half a day may be absorbed at AlistraGIS's discretion where it is genuinely trivial and benefits the product generally. Do not make this a written entitlement — it becomes an expectation of unlimited free work.

## 4. Testing and acceptance

Testing is chargeable work and should be quoted, not absorbed. It is also the
thing that protects both sides when a customer says "this isn't what we asked
for".

| Testing service | Price |
|---|---:|
| User acceptance testing support during onboarding | **Included** — up to 2 sessions |
| Additional UAT support and test-script preparation | **£650 per day** |
| Formal acceptance testing of a customer-hosted environment | **£900 per day**, typically 2 days |
| Data validation testing after a migration | **£850 per day** |
| Regression testing after a bespoke change | **20% of the change cost**, minimum half a day |
| Integration testing with a customer system | **£900 per day** |
| Customer-witnessed or factory acceptance testing | **£750 per day** plus reasonable travel |
| Penetration test or security assessment by a third party | **At cost plus 15%**, arranged on request |

### What is never charged for

Testing AlistraGIS's own work is AlistraGIS's cost. A defect found in delivered
functionality is fixed and re-tested at no charge, and the automated suites that
gate every release are part of maintenance. **The customer pays only for testing
of their own environment, their own data, their own integrations, or a change
they commissioned.**

### Why regression testing is priced as a percentage

A bespoke change to a platform this interconnected can affect things nobody
asked to change. The 20% covers re-running the relevant checks and proving the
rest of the customer's configuration still behaves. Quoting a change without it
means either absorbing that cost or skipping the work, and skipping it is how a
paid change breaks something that was already working.

### Acceptance testing is not optional for customer-hosted

For Model C, the acceptance checklist in the Hosting and Data Responsibility
Schedule must pass before production data is loaded. Quote the testing days
alongside the implementation fee -- a customer who has not budgeted for
acceptance will push to skip it, which is exactly when it matters most.

## 5. Where a change belongs to the roadmap instead

If a requested change improves the product for every customer, it may be better taken as roadmap work at no charge, in exchange for the customer accepting AlistraGIS's timescale rather than theirs.

The rule: **the customer pays for control of timing and specification.** If they need it by a date, in a particular way, it is chargeable. If they simply want it eventually, it can go on the roadmap.

Never write a roadmap item into an Order Form as a contractual deliverable with a date unless it is being paid for and has an acceptance test.

## 6. How releases actually reach customers

Two independent pipelines, with different risk profiles. Anyone doing maintenance needs to know which is which.

- **Frontend:** `git push origin main` → Vercel builds and publishes automatically, live within minutes. There is no manual approval gate.
- **Backend (Cloud Functions):** `npx firebase-tools deploy --only functions --project fibre-gis-v2` — a deliberate, manual command. Deploy by function name to stay within quota rather than deploying all at once.
- **Firestore security rules:** `firebase deploy --only firestore:rules` — separate again, and easy to forget.

Because the frontend auto-deploys and the backend does not, **a release can be half-live**. A frontend change that depends on a new callable must have the backend deployed first, or the feature has to fall back safely until it is. This happened deliberately on 10 September 2026 — see [[Map Performance Work 2026-09-10]].

### Gates before any release

- `npm run typecheck` and `npx tsc --noEmit` in `functions/`
- `npm run test:storage` — the plain-node suite, 1,353 tests as at 10 September 2026
- `npm run test:rules` — the Firestore rules emulator suite, which needs Java 21 ahead of any older JDK on PATH
- `node scripts/run-emulator-integration-tests.mjs` for anything touching storage
- `npm run build`

## 7. Planned maintenance and notice

- Routine updates ship without downtime and without individual notice.
- Where downtime is genuinely required, give **5 working days' notice** and schedule outside UK working hours.
- Emergency security work may be applied immediately, with notice as soon as practicable afterwards.

State these in the Order Form so "you changed it without telling us" is answered by the contract.

## 8. Version and change records

Each customer's file should record: the software version at go-live, dated change requests with their estimates and approvals, any bespoke work and who owns the resulting IP (AlistraGIS, per [[Intellectual Property]], unless the Order Form says otherwise), and dated support-tier changes.

## 9. Before this is used commercially

- [ ] Reconcile the response targets here with [[03 Service Level Agreement]] so the two documents state the same numbers.
- [ ] Confirm the day rates against realistic delivery capacity, not aspiration.
- [ ] Decide the standard support hours and publish them.
- [ ] Confirm the out-of-hours rate is worth being woken up for.
- [ ] Solicitor to confirm the change-control and acceptance wording in [[13 Client Framework Agreement]] clause 15 matches this.

## Related

- [[03 Service Level Agreement]]
- [[Client Pricing Pack]]
- [[Module and Seat Ready Reckoner]]
- [[Data Licensing and Custody Options]]
- [[Map Performance Work 2026-09-10]]
