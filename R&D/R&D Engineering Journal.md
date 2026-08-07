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

### 2026-07-22 to 2026-08-07 — GitHub-evidenced development stream from duct/sub-duct creation onward

**Workstream**  
Duct/sub-duct modelling, cable containment, field/mobile delivery, data integrity, performance, security, refactoring, operational management and commercial-GIS foundations.

**Evidence basis**  
GitHub source-control history in `finchygoldtail/AlistraGIS`. Commit timestamps prove development activity at specific points but do not, by themselves, prove continuous working hours between commits. The detailed day-by-day evidence record is maintained in `R&D/GitHub Development Evidence Timeline.md`.

**Duct/sub-duct origin — 22 July 2026**  
Commit `73fd9b47` — **Add duct and sub-duct route workflow** — introduced duct as a mapped line asset, duct count/diameter/use, cable-to-duct linking and generation of child sub-duct records along duct geometry. Commit `7527ff13` followed by separating duct storage and layers.

**23 July 2026**  
Duct development continued through an evidenced commit window of approximately 15:58–19:39 with the duct designer, route visibility, workspace duct layer/menu/count fixes, overview visibility, duct click/edit behaviour and workspace editor wiring.

**24 July 2026**  
A concentrated evidenced window of approximately 14:07–18:45 developed cable containment inside ducts/sub-ducts, assigned-cable display, routing along duct geometry, nested/leaf sub-duct rendering, cable reconciliation, duct capacity warnings and design visibility.

**27–29 July 2026**  
Further integration added duct counting into the asset register and route splitting/scoping at joints.

**2–3 August 2026**  
Work extended duct progress into production/completed sections and added route-splitting robustness, repeated-vertex handling, joint insertion from duct routes, coordinate normalisation, mobile duct workflows, QGIS metadata, mobile production classification fixes, network schematic enhancements, mobile/tablet field improvements and photo/evidence workflows.

**4 August 2026**  
Major reliability, performance and security work addressed silent photo/edit data loss, targeted per-asset writes instead of whole-project rewrites, Storage cleanup/compression, incremental exchange writes, viewport culling, KML import issues, snap throttling, duplicate audit writes, resumable uploads, persistent failed-upload recovery and server-managed audit-trail writes.

**5 August 2026**  
Large-scale refactoring and hardening across JointMapManager, ProjectWorkspace, UserManagementPanel, DistributionPointEditor, WorkspaceBuild, ExchangeDesigner, WorkspaceMap, AssetMarkersLayer, StreetCabDesigner and joint-map workspace handlers. A key commit (`9739be4d`) reduced `JointMapManager.tsx` from 4,077 to 2,875 lines and extracted the autosave, pending-save recovery, context-add handling, duct-joint insertion and approximately 527-line duct/sub-duct/cable creation workflow. Ticketing/helpdesk, high-severity audit fixes, permission hardening, dead-tab wiring and runtime crash fixes were also implemented.

**6 August 2026**  
Further map render/memoisation work, ticket hardening, QA/lifecycle/report fixes and the Plant & Equipment / Vehicle Management / Smart Work Pack implementation. Commit `cd8ca13f` records company-wide plant/equipment and vehicle registers with check-in/out, faults, inspections/services/calibration, compliance alerts, QR labels, CSV/Excel workflows, crews, documents and Work Pack lifecycle/readiness functionality. The commit records 151 passing unit tests and clean typecheck/build.

**7 August 2026**  
Development continued on supervisor role, single-session enforcement, employee credentials, vehicle QR scanning, fleet functionality, as-built generation, module entitlement filtering, User Register fixes, moving Plant/Vehicle/Employees into Management, batch import/security fixes, shared styling and additional Round 4 audit fixes. Alistair contemporaneously recorded starting work at 09:00 and working through the day; the cost/time register records a 10.5-hour elapsed window to approximately 19:30 pending break reconciliation.

**What was learned**  
The source-control trail shows that the duct/sub-duct model became a foundation for wider network, production, field, storage, topology and later commercial workflows. It also shows that substantial effort was required not just to add features but to remove entanglement, reduce unsafe write patterns, protect field data, improve large-map performance and harden permission/audit boundaries.

**R&D treatment caution**  
Not all commits or hours automatically qualify as R&D. Routine UI changes, normal feature development and ordinary bug fixing should be separated from work directly resolving technological uncertainty. GitHub evidence is used to corroborate activity and workstream, not to manufacture unsupported hours.

**Evidence links**  
- `R&D/GitHub Development Evidence Timeline.md`
- `R&D/AI and Development Cost Register.md`
- Repository commits including `73fd9b47`, `9739be4d`, `cd8ca13f`, `4626201e`, `905c8e96`, `39f91285`, `125262ad`
- AI coding sessions and dated ChatGPT/Claude records where available

---

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

### 2026-08-05 to 2026-08-07 — Duct/sub-duct billing model and map-driven commercial takeoff design

**Workstream**  
Commercial GIS, duct/sub-duct quantity modelling, BOQ/material derivation and API architecture.

**Technical uncertainty**  
The development work investigated how AlistraGIS could use the live GIS network as the commercial source of truth rather than requiring quantities to be rebuilt manually in spreadsheets. Key uncertainties included how duct and sub-duct quantities should be represented for billing, how arbitrary geographic selections should be converted into accurate quantities without counting entire assets that only partially cross a selected area, and how mapped primary assets could be expanded into the non-mapped sundries required for a realistic BOQ.

**Baseline / existing capability**  
AlistraGIS already contained substantial surrounding capability including mapped fibre assets, commercial/BOQ direction, stock functionality, production information, build-partner concepts, reporting and rate-card functionality. The missing connection was a reliable map-area selection and spatial takeoff layer that could feed those existing systems. A simple asset count would also omit materials such as joint glands, MOBRA arms, Kit 1A, splice trays, mounting hardware, couplers, plugs, labels and other sundries.

**Hypothesis or proposed advance**  
Use a selected or user-drawn GIS polygon to create a deterministic commercial takeoff. Point assets would be included by spatial relationship; linear assets such as duct, sub-duct and cable would be clipped to the commercial boundary and only the geometry inside the polygon would be measured. Primary asset quantities would then pass through a configurable, versioned asset-recipe/material engine to derive sundries before using existing stock, BOQ and rate-card functionality.

**Work performed**  
- Developed the duct and sub-duct billing concept so mapped route quantities can support commercial measurement.
- Defined a commercial area-selection workflow using either existing project/AG polygons or temporary user-drawn polygons.
- Defined spatial clipping requirements for duct, sub-duct, cable and other linear assets so partial intersections are measured rather than charging the full parent asset.
- Defined point-asset inclusion and manual inclusion/exclusion behaviour for chambers, joints, poles, DPs/CBTs and premises.
- Identified the need for duplicate-scope protection so the same asset or overlapping linear segment is not inadvertently allocated to multiple active subcontract packages.
- Designed an Asset Recipe / Sundries Matrix to convert primary assets into full material requirements, including joint closures, MOBRA arms, gland kits, Kit 1A, splice trays, mounting kits, labels, fixings, duct couplers/plugs, draw rope and configurable consumables.
- Defined recipe rule types including exact quantity, per asset, per cable entry, per metre, conditional/variant rules, percentage allowances and manual allowances.
- Defined recipe versioning so later recipe changes cannot alter historical issued packages.
- Defined material-specific waste, pack/drum rounding and procurement quantities separately from the raw design requirement.
- Defined client-supplied, build-partner-supplied, free-issue, included-in-rate and separately chargeable material ownership states to reduce double charging.
- Defined stock reservation against awarded commercial packages.
- Defined Estimated, Contracted, Actual and Certified commercial values as separate lifecycle states so production completion does not itself authorise payment.
- Defined immutable commercial-package snapshots containing the polygon, included/excluded asset references, quantities, recipe version, rate-card version and commercial totals.
- Defined manual quantity overrides with retention of original calculated quantity, reason, user and timestamp.
- Designed variation records and advisory comparison between contracted snapshots and current as-built/production data to identify potential changes without automatically creating or approving claims.
- Designed comparison of multiple build-partner rate cards against one takeoff before award.
- Defined Excel export requirements using the saved commercial snapshot, with sheets for summary, primary assets, materials/sundries, stock requirement, BOQ/rate card, build-partner cost, client billing, margin, overrides/audit and variations.
- Defined PDF and map-scope export concepts for subcontract issue/approval packs.
- Reviewed API boundaries and selected a bounded-service approach: Commercial Takeoff, Materials/Recipes and Commercial Packages as distinct logical responsibilities, while extending existing Stock/BOQ and Reports capabilities rather than duplicating them. Logical API boundaries do not require separate deployments.
- Added implementation safeguards covering geometry accuracy, duplicate counting, historic version locking, permissions, excessive reads/writes, audit-log volume, concurrency and large-dataset performance.

**Result**  
Design/architecture stage completed for the commercial takeoff capability. The work established a route from live GIS geometry to commercial quantities and a method for including derived sundries that are not themselves drawn on the map. Implementation and validation remain outstanding.

**What was learned**  
A map polygon alone is insufficient for a commercially useful takeoff. The spatial takeoff must distinguish point and linear geometry, clip partial lines accurately, prevent overlapping commercial allocation, and then expand mapped assets through versioned recipes. Historical commercial packages also require frozen calculation inputs; recalculating an old package from current GIS, recipe or rate-card data would make the commercial record non-reproducible.

**Remaining uncertainty**  
- Accuracy and performance of polygon/line clipping against large real-world project datasets.
- Boundary rules for points lying exactly on a polygon edge.
- Robust detection of overlapping portions of the same linear asset across active packages.
- Final business recipe quantities for each joint/chamber/duct/cable variant.
- Correct handling of cable drum, duct bundle and other supplier-specific order rounding.
- Integration details with the current production, BOQ, stock, rate-card and reporting implementations after repository inspection.
- Permission model for commercially sensitive rates, costs and margin.

**People involved and time spent**  
- Alistair Grantham — product definition, telecom-domain rules, commercial workflow design, duct/sub-duct billing requirements, review and AI-assisted technical design.
- Exact hours: **to be confirmed from actual working records/session history before being used for payroll, cost allocation or an R&D claim.** No unsupported hour estimate has been entered.

**Evidence links**  
- Design record: ChatGPT development discussions dated 5–7 August 2026 covering AlistraGIS production/commercial architecture, duct/sub-duct billing, area takeoff, sundries, exports and API boundaries.
- Vault: R&D Engineering Journal and related R&D registers.
- GitHub development evidence timeline: source-control backfill from 22 July onward.
- Test output: pending implementation.
- Invoice / cost record: R&D Costs — director/developer time to be populated from actual hours and remuneration basis.

**Next action**  
Implement against the existing AlistraGIS architecture after repository inspection, then record actual development/test time separately from product/commercial planning time. Add spatial unit tests, material-recipe tests, version-lock tests, permission tests and export reproducibility tests. Link the resulting commits, test evidence and deployment records back to this entry.

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