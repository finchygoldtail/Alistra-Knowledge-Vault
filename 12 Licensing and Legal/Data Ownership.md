---
title: Data Ownership
type: legal
status: draft-for-solicitor-review
owner: Alistair
created: 2026-08-02
updated: 2026-09-10
tags: [legal, data, ownership, ip]
related: ["[[Data Licensing and Custody Options]]", "[[13 Client Framework Agreement]]", "[[17 Customer Data Processing Agreement]]", "[[03 GDPR Data Register]]", "[[Intellectual Property]]"]
---

# Data Ownership

> **Draft for UK technology solicitor review.** This sets out the working position AlistraGIS intends to take. It needs confirming against the executed Framework Agreement before it is relied on with a customer.

Ownership and data protection are different questions and must not be run together. **Ownership** is who the data belongs to. **Controller/processor** is who decides why personal data is processed. A customer can own data that AlistraGIS processes, and AlistraGIS can own aggregated statistics derived from data it does not own. Both are addressed below; the data-protection roles live in [[17 Customer Data Processing Agreement]].

## 1. Categories of data, and who owns each

| Category | Examples | Owner |
|---|---|---|
| **Customer Data** | Network design, asset records, geometry, areas and projects, survey and QA records, production records, photographs, documents, job packs, commercial records | **Customer** |
| **Customer Personal Data** | Customer's employee and crew records, credentials, contact details, location records | **Customer** (as controller) |
| **Third-Party Licensed Data** | Ordnance Survey products, Openreach PIA records, address/UPRN data, purchased datasets | **The third-party licensor**, used under the Customer's own licence |
| **Base Mapping** | Esri / OpenStreetMap tiles rendered in the product | **The tile provider**, under AlistraGIS's arrangements, attribution preserved |
| **Platform Software and Materials** | Source code, database schema, APIs, interface, documentation, templates, report and job-sheet layouts | **AlistraGIS** |
| **Configuration** | Customer-specific settings, roles, naming conventions, workflow configuration | **AlistraGIS owns the configurable capability; the Customer owns its own configuration values** |
| **Aggregated Statistics** | Anonymised platform usage, volumes, performance metrics | **AlistraGIS**, provided the data is genuinely anonymised and not attributable to any customer or individual |
| **Support and Audit Records** | Tickets, change logs, access logs, audit trails | **AlistraGIS owns the records; the Customer has a right of access to those concerning it** |

## 2. Customer Data — the core position

**The Customer owns its Customer Data.** Nothing in a subscription, an Order Form or the act of uploading transfers ownership to AlistraGIS.

AlistraGIS takes a **limited, non-exclusive licence** to use Customer Data solely to:

- host, store, process, transmit and display it in the provision of the service;
- back it up and restore it;
- provide support, diagnose faults and investigate incidents;
- generate outputs, exports and reports the Customer requests;
- comply with a legal obligation.

That licence lasts only as long as needed for those purposes and ends on deletion under the exit terms.

**AlistraGIS will not:** sell Customer Data, license it to a third party, use it to provide services to another customer, publish it, or use it to train third-party AI models, without separate written agreement.

## 3. Outputs and derived records

Exports, reports, job packs, as-built drawings, handover documents and job sheets generated from Customer Data are **the Customer's**, even though the templates and generating software are AlistraGIS's.

The distinction: the Customer owns the *content*; AlistraGIS owns the *thing that produced it*. A customer may use, copy and issue its own job sheets freely. It may not extract the layout, template or generating logic and rebuild it elsewhere.

## 4. Aggregated and anonymised statistics

AlistraGIS may derive aggregated statistics for operating and improving the platform — how many assets a typical estate holds, how long an operation takes, which features are used.

Conditions that should be stated in the Order Form:

1. Genuinely anonymised, with no customer, project, site, individual or commercially sensitive value identifiable or reasonably re-identifiable.
2. Never used to disclose one customer's commercial position to another.
3. Capable of being disabled for a customer that objects.

Anything short of genuine anonymisation is Customer Data and Customer Personal Data, and this clause does not apply to it.

## 5. Artificial intelligence

Customer Data must not be sent to a third-party AI provider unless:

- the Order Form says so explicitly;
- the provider is on the [[Subprocessor Register]] with a signed DPA;
- region, security and retention terms have been checked; and
- the provider does not train its models on the data.

Until each of those is satisfied for a given feature, the default is that Customer Data does not leave the platform. See [[Client Pricing Pack]] section 10 for the commercial structure.

## 6. Third-party licensed data

AlistraGIS does not sublicense data it does not own. Ordnance Survey products, Openreach PIA records and purchased address data are held on the Customer's behalf **under the Customer's own licence**, and the Customer is responsible for holding the rights to supply them.

The Framework Agreement should require the Customer to warrant it has the right to upload what it uploads, and to indemnify AlistraGIS against a third-party claim that it did not. See [[13 Client Framework Agreement]] clause 16.

## 7. Ownership across the hosting models

Ownership does **not** change with the hosting model. What changes is custody and operational responsibility.

| | Who owns Customer Data | Who holds it | Who is responsible for its availability |
|---|---|---|---|
| Model A — AlistraGIS shared | Customer | AlistraGIS | AlistraGIS |
| Model B — AlistraGIS dedicated | Customer | AlistraGIS | AlistraGIS |
| Model C — Customer-hosted | Customer | Customer | **Customer**, for the infrastructure; AlistraGIS for the application |

Model C is the one to be careful with: if the customer's own database is unavailable or unrecoverable, that is the customer's risk, and the Order Form must say so. See [[15 Hosting and Data Responsibility Schedule]].

## 8. Exit and return

On termination, and stated plainly in sales conversations because it removes an objection:

1. The Customer gets **one full export in open, documented formats** at no charge — GeoJSON/KML geometry, CSV records, original uploaded files.
2. A reasonable window to retrieve it — **30 days** is the working position.
3. After that window, and on the Customer's instruction, AlistraGIS deletes Customer Data from live systems and confirms deletion in writing.
4. Backups age out on their documented cycle rather than being surgically edited; the retention period should be stated rather than implied. See [[Data Retention Schedule]].
5. Bespoke exit formats or migration help are chargeable — see [[Data Licensing and Custody Options]] section 8.

## 9. What still needs deciding

- [ ] Solicitor to confirm the ownership/licence split survives review, particularly outputs and aggregated statistics.
- [ ] Confirm the 30-day retrieval window and the backup ageing period against [[Data Retention Schedule]].
- [ ] Decide whether the anonymised-statistics right is offered as opt-out (recommended) or removed entirely for a first client who queries it.
- [ ] Confirm the customer warranty and indemnity wording for third-party data.
- [ ] Confirm insurance covers a claim arising from loss or corruption of Customer Data.

## Related

- [[Data Licensing and Custody Options]]
- [[Intellectual Property]]
- [[13 Client Framework Agreement]]
- [[17 Customer Data Processing Agreement]]
- [[03 GDPR Data Register]]
- [[Data Retention Schedule]]
- [[GDPR Responsibilities]]
