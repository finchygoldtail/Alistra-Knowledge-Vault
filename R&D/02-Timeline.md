# AlistraGIS Development Timeline

> This is a reconstructed timeline from project discussions and known decisions. Exact dates should be cross-checked against Git commits, deployment history, invoices and test records.

## Early platform development — before July 2026

- Established the core React/TypeScript/Vite application.
- Introduced Leaflet/react-leaflet mapping with editable fibre assets.
- Used Firebase Authentication, Firestore and Storage for the first working architecture.
- Developed role-based access for administrators, super users, survey, build and maintenance users.
- Created map layers for exchanges, fibrehoods, areas, joints, cabinets, poles, chambers, homes, ducts, cables and distribution points.
- Added metadata for asset creation, update history and revision control.
- Developed map tools for selection, measuring, drawing cables and drawing areas.
- Investigated snapping, road routing and map-save behaviour.

## Core operational expansion

- Added Openreach/PIA-related overlays and evidence requirements.
- Defined PIA status workflows and colour-coded quality states.
- Developed the commercial dashboard foundation, job-pack editor and map-linked project documentation.
- Separated distribution-network assets from global core/feeder assets.
- Modelled exchange, EBCL, feeder, WDM, splitter and meet-me arrangements.
- Began formalising fibre continuity and through-splice records.

## Performance and reliability investigations

- Identified map slowdown as asset volumes increased.
- Investigated bounded reads, chunked asset storage and alternatives to loading an entire dataset into the viewport.
- Considered autosave but retained controlled map saves because of Firestore write-volume and conflict concerns.
- Diagnosed UI and asset-editor regressions, duplicate React keys and issues caused by inconsistent asset identity.
- Tested a VPS/API storage approach, but reverted to Firestore after saved assets behaved unpredictably and required unsuitable upload workflows.

## Mobile and tablet development — July 2026

- Explored a dedicated mobile shell, then moved back towards desktop-feature parity for field users.
- Documented tablet and mobile defects involving off-screen drawers, stuck landscape panels, overlay conflicts, duplicated login views and map controls.
- Restricted map drawing to administrators/super administrators while retaining field tools such as navigation, measuring and layer toggling for other users.
- Added the requirement for tap-to-navigation through external mapping applications.

## Data, tenancy and enterprise architecture — July 2026

- Raised concerns about employer-owned data and decided to use test data until ownership and hosting arrangements were clear.
- Defined multi-company/client requirements and the need for tenant isolation.
- Added a requirement to capture each client's preferred storage platform, including Firebase, Microsoft/Azure or AWS-based options.
- Began moving from a single application towards separate modules and service APIs.
- Defined an API catalogue covering Map, Projects, Assets, Audits, Workspace, Production, Health & Safety, Topology, Openreach and Files.
- Considered packaging the platform for licensing, client hosting and full API sale.

## Workspace and product redesign — late July to early August 2026

- Identified that the existing Build tab had become overloaded.
- Proposed top-level areas: Overview, Design, Production, Survey, PIA & Permits, QA/Walk-off, Commercial, H&S, Handover and Admin/Utilities.
- Elevated Production into a first-class module covering daily returns, crews, blockers, duct/cable metres, splice progress, evidence and reporting.
- Renamed the project workspace concept to Alistra Mission Control.
- Designed a more modular user experience while retaining a light operational map.

## Security and compliance work — early August 2026

- Reviewed risks in uncapped asset-view logging and duplicate change-log implementations.
- Identified that audit/change-log entries required stronger server-side protection and append-only rules.
- Added a requirement for a support/ticketing process for password changes, upgrades and controlled administrative requests.
- Began a GDPR roadmap covering access, retention, audit trails, security controls and client data responsibilities.
- Added the requirement to prevent multiple simultaneous sessions from consuming a single paid user seat.

## AI and automation research

- Defined the FRIDAY AI concept for code inspection, defect detection and engineering assistance.
- Explored automated network design within a polygon, fibre-capacity planning and spare-fibre constraints.
- Recognised that using a general AI API alone is not necessarily an advance; qualifying work would need to focus on custom engineering logic, constraint solving, validation or integration uncertainty.

## Company and claim boundary

- AlistraGIS Ltd was incorporated in late July 2026.
- The first company accounting period is expected to end around 31 July 2027.
- Development evidence from before incorporation should be retained, but company expenditure and activities must be separated from personally incurred pre-incorporation work.

## Timeline evidence still required

- Confirm incorporation date and accounting-period dates.
- Export Git commit history with dates and authors.
- Export Vercel deployment history.
- Gather Firebase, GitHub, Vercel and AI-service invoices.
- Link major bugs, prototypes and architecture changes to commits or screenshots.
- Record dates when each technological uncertainty started and ended.
