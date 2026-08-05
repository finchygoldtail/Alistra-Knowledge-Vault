# AlistraGIS R&D Engineering Journal

> Purpose: contemporaneous technical record supporting the AlistraGIS research and development work. Update this journal whenever a material technical uncertainty is investigated, tested, resolved, rejected or carried forward.

## Project details

- **Project:** AlistraGIS
- **Company:** AlistraGIS
- **Development status:** Active development, moving toward structured testing
- **Accounting period:** Expected to end around July 2027
- **Journal started:** 5 August 2026
- **Primary technical areas:** GIS performance, fibre-network topology, field workflows, multi-tenant data architecture, API separation, mobile/tablet delivery, import/export compatibility, security and auditability

## What the project is trying to achieve

AlistraGIS is intended to provide a single operational platform for telecom network design, field delivery, production, quality assurance, PIA, permits, health and safety, handover, asset management and fibre topology. The development work goes beyond assembling standard forms because the platform must maintain spatial, operational and network-topology relationships while remaining usable in real-time by office and field users.

## Main technological uncertainties

1. Whether large telecom GIS datasets can be displayed, edited and synchronised in real time without degrading field usability.
2. Whether fibre topology, splitter relationships, feeder continuity and through-splice logic can be represented in a reliable, auditable data model.
3. Whether tenant, company, project and area boundaries can be enforced consistently across authentication, API and storage layers.
4. Whether GIS imports from KML, KMZ, GPKG and GeoJSON can be normalised without corrupting geometry, attributes or map performance.
5. Whether mobile and tablet users can use a reduced field workflow while retaining sufficient desktop parity and permission controls.
6. Whether client-selected storage providers can be supported without weakening data isolation, audit logging or platform consistency.
7. Whether event logging, evidence uploads and asset history can remain complete without creating excessive database writes or cost.

## Engineering journal entries

### 2026-08-05 — R&D record structure established

**Problem / uncertainty**  
Historic development evidence existed across source control, ChatGPT/Codex discussions, screenshots, renders, test data and implementation notes, but it had not been consolidated into a claim-ready technical record.

**Work undertaken**  
Created the R&D Engineering Journal, Costs, Innovation Register, Risk Register and Evidence Register inside the Alistra Knowledge Vault. Defined a structure for linking technical uncertainties, experiments, costs, risks and supporting evidence.

**Outcome**  
A repeatable evidence framework now exists. Historic entries still need to be backfilled from GitHub history, design conversations, deployment records and invoices.

**Next action**  
Backfill one entry for every material development stream and link each entry to commits, screenshots, test results, invoices and decision records.

---

### Historical workstreams to backfill

Create dated entries for the following workstreams using the template below:

- Firestore chunking and bounded map reads
- Real-time multi-user asset synchronisation
- Map performance with large asset volumes
- Fibre topology and continuity modelling
- Exchange, WDM, splitter, feeder and meet-me modelling
- KML, KMZ, GPKG and GeoJSON import handling
- Mobile and tablet field interface
- Role and permission architecture
- Concurrent-session and licensed-seat controls
- PIA evidence and status workflow
- Production, route-progress and daily-return workflows
- Project Workspace / Mission Control modularisation
- API gateway and service separation
- Multi-company and client-selected storage architecture
- Audit and change-log hardening
- Write-volume and cost control
- Automated or assisted network design

## Entry template

### YYYY-MM-DD — Title

**Workstream**  

**Technical uncertainty**  
What could not readily be deduced by a competent professional at the start?

**Baseline / existing capability**  
What standard technology, library or known approach was available?

**Hypothesis or proposed advance**  
What improvement or new capability was being attempted?

**Work performed**  
Designs, prototypes, code changes, experiments, tests and reviews.

**Result**  
Pass, fail, partial success or inconclusive.

**What was learned**  

**Remaining uncertainty**  

**People involved and time spent**  

**Evidence links**  
- Commit / PR:
- Screenshot / render:
- Test output:
- Design note:
- Invoice / cost record:

**Next action**  

## Monthly review checklist

- Add all material experiments and failed approaches.
- Record time spent by person and workstream.
- Link costs to qualifying activities rather than the whole business.
- Preserve source-control, deployment and test evidence.
- Separate routine product work from work addressing genuine technological uncertainty.
- Record the date an uncertainty was resolved or abandoned.

## Important note

This journal is an engineering record, not a final tax opinion. The qualifying treatment of activities and expenditure should be reviewed with an accountant or R&D tax adviser before submission.