# AlistraGIS R&D Costs

> Purpose: record expenditure connected with AlistraGIS research and development activities. Do not assume every development or business cost qualifies. Allocation and eligibility should be reviewed before any claim is submitted.

## Claim period

- **Expected accounting period end:** Around July 2027
- **Record started:** 5 August 2026
- **Currency:** GBP
- **Basis:** Actual expenditure supported by invoices, payroll records, bank statements, contracts and reasonable apportionment calculations

## Cost recording principles

1. Record costs as they arise rather than reconstructing them at year end.
2. Link every cost to one or more R&D workstreams and journal entries.
3. Separate qualifying technical work from routine development, sales, administration, hosting for live customers and general business activity.
4. Keep the original invoice or payroll evidence.
5. Document the allocation method where only part of a cost relates to R&D.
6. Do not include estimates in the final claim unless they are supported by a reasonable and documented methodology.

## Cost register

| Date | Supplier / person | Cost category | Description | Gross cost | R&D allocation % | Potential R&D amount | Workstream | Evidence reference | Status / notes |
|---|---|---|---|---:|---:|---:|---|---|---|
| 2026-08-05 | Alistair Grantham | Director / developer time | Establish R&D evidence framework and registers | To calculate | To review | To calculate | R&D governance and evidence | R&D Engineering Journal entry 2026-08-05 | Record actual hours and remuneration basis |
| 2026-08-05 to 2026-08-07 | Alistair Grantham | Director / developer time | Duct/sub-duct billing model; map-driven commercial takeoff; spatial clipping requirements; asset recipe/sundries model; stock/waste/reservation rules; commercial package lifecycle; variations; Excel/PDF/map export design; API boundary design and technical risk review | To calculate | To review | To calculate | Commercial GIS / spatial takeoff / API architecture | R&D Engineering Journal entry 2026-08-05 to 2026-08-07 | Actual hours not yet evidenced. Record from working/session records before any cost or R&D claim calculation; separate qualifying technical investigation from routine commercial/product planning. |
| 2026-07-22 to 2026-08-07 | Alistair Grantham | Director / developer time | Source-control-evidenced development from original duct/sub-duct workflow through cable containment, mobile/tablet delivery, reliability/performance/security hardening, large-scale refactoring, ticketing, plant/equipment, vehicles, employees, crews and Smart Work Packs | To calculate | To review | To calculate | Multiple technical workstreams | GitHub Development Evidence Timeline + application commits | Do not convert commit spans directly into hours; reconcile with contemporaneous records, AI sessions and actual working time. |

## Development time awaiting reconciliation

The following recent AlistraGIS work has been identified for time reconstruction. This section is an evidence queue, not a claim of hours.

| Period | Person | Work identified | Hours | Evidence status | Allocation note |
|---|---|---|---:|---|---|
| 2026-07-22 | Alistair Grantham | Original duct/sub-duct route workflow and storage/layer separation | To confirm | GitHub commits `73fd9b47`, `7527ff13` | Technical design/implementation/testing time before first commit unknown; reconstruct from conversations/AI sessions where available |
| 2026-07-23 | Alistair Grantham | Duct designer, route visibility, workspace layers/counts, duct clicks/edit locking and workspace duct-editor wiring | To confirm | GitHub activity window approx. 15:58–19:39 | 3h40m is an elapsed commit window, not automatically worked/claimable hours |
| 2026-07-24 | Alistair Grantham | Cable containment in ducts/sub-ducts, route sync, nested/leaf sub-duct rendering, capacity warnings and design visibility | To confirm | GitHub activity window approx. 14:07–18:45 | 4h38m is an elapsed commit window, not automatically worked/claimable hours |
| 2026-07-27 to 2026-07-29 | Alistair Grantham | Duct asset-register integration, cable scoping and splitting routes at joints | To confirm | GitHub commit evidence | Reconstruct only where stronger time evidence exists |
| 2026-08-02 to 2026-08-03 | Alistair Grantham | Duct progress, route splitting, field/mobile workflows, QGIS metadata, production fixes, network schematic and photo/evidence flows | To confirm | Dense GitHub history across day/evening | Use GitHub as supporting evidence; reconcile with session history |
| 2026-08-04 | Alistair Grantham | Data-loss prevention, targeted saves, Firestore/Storage cost reduction, KML fixes, performance, upload reliability and audit/security hardening | To confirm | Multiple detailed GitHub commits | Split routine defect correction from technological uncertainty work |
| 2026-08-05 | Alistair Grantham | Large-scale refactor across core files, map autosave/extractions, security fixes, ticketing and workspace wiring | To confirm | Strong GitHub commit trail incl. `9739be4d` | Substantial refactor effort evidenced; exact hours still need reconstruction |
| 2026-08-06 | Alistair Grantham | QA/lifecycle/report fixes, map memoisation, ticket hardening, Plant & Equipment, Vehicle Management, crews/documents and Smart Work Pack | To confirm | GitHub incl. `cd8ca13f`; 151 tests and clean builds recorded | Separate feature work from deeper technical uncertainty/testing for R&D allocation |
| 2026-08-07 | Alistair Grantham | Vehicles/equipment/employees, supervisor/session controls, vehicle QR, fleet/as-built, entitlement/admin fixes and Round 4 audit remediation | 10.5h elapsed 09:00–~19:30 before breaks | Contemporaneous user record + GitHub commits `4626201e`, `905c8e96`, `1090e918`, `39f91285`, `125262ad` + £24 Claude spend | Reconcile breaks; then split technical R&D, qualifying indirect and routine product work |
| 2026-08-05 to 2026-08-07 | Alistair Grantham | Duct and sub-duct commercial/billing modelling; commercial map-area takeoff; spatial line clipping; derived material/sundry recipes; recipe/version locking; stock waste and reservation; package snapshots; Estimated/Contracted/Actual/Certified lifecycle; duplicate allocation protection; build-partner rate comparison; variation/change detection; XLSX/PDF/map export requirements; bounded API/service architecture | To confirm | ChatGPT design-session evidence identified; application commit/test evidence to link as implementation proceeds | Split technical R&D investigation/testing from routine product definition, pricing/commercial administration and other non-qualifying work before adviser review |

## Time reconstruction evidence hierarchy

1. Contemporaneous start/finish/break records supplied by Alistair.
2. AI coding-session usage and provider billing aligned to the workstream.
3. GitHub commit and CI/build timestamps aligned to the same workstream.
4. Dated ChatGPT/Claude/Codex conversations and design notes.
5. First-to-last commit spans as supporting context only.
6. Never multiply commit count by an assumed number of minutes/hours.

## Categories to track

### Staffing and director time

Record:

- Name and role
- Employment or director status
- Gross pay and relevant employer costs where applicable
- Total working hours for the period
- Hours spent directly resolving technological uncertainties
- Hours spent on qualifying indirect activities, where supportable
- Non-R&D time excluded
- Calculation method and supporting records

| Month | Person | Total paid hours | Direct R&D hours | Qualifying indirect hours | R&D % | Payroll cost | Potential R&D amount | Evidence |
|---|---|---:|---:|---:|---:|---:|---:|---|
| | | | | | | | | |

### Software, cloud and computing

Potentially relevant items may include development and test use of:

- Firebase / Google Cloud
- Vercel
- GitHub
- Mapping and geospatial services
- AI coding or development tools
- Test environments
- Logging and monitoring
- Storage used for prototypes and test evidence
- Development hardware or consumable computing resources, subject to advice on treatment

| Date | Supplier | Service | Period | Total cost | Development/test allocation | Live/business allocation | Workstream | Invoice link | Notes |
|---|---|---|---|---:|---:|---:|---|---|---|
| | | | | | | | | | |

### Subcontractors and externally provided workers

Record contracts, location, relationship, work performed, payment date, connected-party status and whether the work directly addressed an R&D uncertainty.

| Supplier | Contract period | Work performed | Total paid | R&D allocation | Evidence | Adviser review |
|---|---|---|---:|---:|---|---|
| | | | | | | |

### Data, licences and consumables

Record any datasets, API usage, test licences, mapping credits or other consumable items used directly in experimentation.

| Date | Item | Purpose | Cost | R&D workstream | Allocation basis | Evidence |
|---|---|---|---:|---|---|---|
| | | | | | | |

## Current cost sources to gather

- GitHub subscription invoices
- Vercel invoices and domain costs separated from development hosting
- Firebase / Google Cloud billing exports
- Map provider invoices or usage statements
- ChatGPT, Codex or other AI development-tool invoices
- Claude / Claude Code invoices and credit receipts
- Domain and email costs, noting that general business costs may not qualify
- Computer hardware and software purchase records
- Accountant, solicitor and commercial-advice fees, normally tracked separately from technical R&D costs
- Any subcontractor invoices
- Payroll, director remuneration and time records

## Monthly cost close

At the end of each month:

1. Export invoices and billing reports.
2. Add each item to the register.
3. Allocate it to a workstream.
4. Link it to engineering journal and evidence-register entries.
5. Mark uncertain items for accountant review.
6. Reconcile totals to accounting records.

## Summary by workstream

| Workstream | Recorded cost | Potential R&D allocation | Evidence completeness | Review status |
|---|---:|---:|---|---|
| Duct/sub-duct and cable containment | | | Strong GitHub activity evidence; hours pending | Adviser review required |
| GIS performance and synchronisation | | | GitHub activity evidence identified | Adviser review required |
| Fibre topology and continuity | | | GitHub activity evidence identified | Adviser review required |
| Import and format normalisation | | | GitHub activity evidence identified | Adviser review required |
| Mobile and tablet field delivery | | | Strong GitHub activity evidence; hours pending | Adviser review required |
| API and multi-tenant architecture | | | Work identified | Adviser review required |
| Security, audit and data integrity | | | Strong GitHub activity evidence; hours pending | Adviser review required |
| Refactoring / maintainability | | | Strong GitHub activity evidence; hours pending | Split routine vs qualifying work |
| Plant / vehicles / employees / crews | £24 Claude usage linked to 7 Aug work; labour cost pending | | Strong current evidence | Adviser review required |
| Automated network design | | | Not started | |
| Commercial GIS and spatial takeoff | | | Time/work identified; hours pending reconciliation | Adviser review required |

## Adviser review questions

- Which staffing and director-remuneration elements are claimable for the period?
- How should mixed development/live cloud costs be apportioned?
- Which software and data costs fall within the applicable scheme rules for this accounting period?
- Are any subcontractors connected parties or overseas providers requiring special treatment?
- What records are required for work performed before AlistraGIS was incorporated?
- Should any pre-incorporation expenditure be treated separately?
- How should AI coding-tool subscriptions/credits be apportioned where they support both qualifying and routine development?

## Important note

This register identifies potential R&D expenditure only. Final eligibility, scheme selection and tax treatment must be confirmed using the rules applying to the company and accounting period.