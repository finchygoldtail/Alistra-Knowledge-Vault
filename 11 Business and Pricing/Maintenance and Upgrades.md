---
title: Maintenance and Upgrades
type: business
status: draft
owner: Alistair
created: 2026-08-02
updated: 2026-09-05
tags: [maintenance, pricing]
---

# Maintenance and Upgrades

## What "maintenance" actually covers today

Deployment is two independent pipelines, both already live:

- **Frontend**: `git push origin main` → Vercel builds and publishes automatically. No manual deploy step.
- **Backend**: `firebase deploy --only functions` — a manual, explicit action; Cloud Functions do not auto-deploy from a git push the way the frontend does. Anyone doing "maintenance" needs to know these are two separate release mechanisms with two separate risk profiles — a bad frontend push is live in minutes, a backend deploy needs a deliberate command.
- Automated checks that exist and should gate any release: `npm run typecheck`, the plain-node test suite (`npm run test:storage`, 600+ tests as of 2026-09-05), and the firestore.rules emulator suite (`npm run test:rules` — needs Java 21 on PATH ahead of any older JDK, a real local gotcha, not a CI concern).

## What a support/maintenance tier could reasonably promise

| Level | Bug fixes | New features | Response time | Illustrative price |
|---|---|---|---|---|
| Standard | Included, best-effort | Roadmap-driven, not guaranteed | Business hours | **[SET PRICE]** or bundled into subscription |
| Priority | Included, prioritised | Some influence over roadmap | Same-day acknowledgement | **[SET PRICE]** uplift |
| Enterprise | Included, prioritised | Negotiated custom work | Named contact, defined SLA | **[SET PRICE]**, contract-specific |

This should be cross-referenced against [[03 Service Level Agreement]] before being sold as a defined SLA — that document already has the legal shape (response times, uptime commitments); this page just needs to agree with it on actual numbers rather than duplicating a second, possibly conflicting set.

## Related

- [[03 Service Level Agreement]] — where committed response times and uptime actually need to live.
- [[Active Bugs]]
- [[Codex Backlog]]
- [[Vercel Deployment]]
- [[Pricing Models]]
