# AlistraGIS Technical Uncertainties

> These are candidate technological uncertainties for investigation and evidence gathering. They must be tested against HMRC's current rules and supported by contemporaneous records. Commercial difficulty, normal configuration and routine coding are not enough on their own.

## 1. Scalable real-time GIS rendering and storage

### Advance sought

A browser-based GIS capable of displaying and editing a large, live fibre-network dataset while remaining responsive for multiple users and controlling database usage.

### Uncertainty

It was not clear how to structure, query and render the required number of heterogeneous map assets without loading excessive data, freezing the browser, creating duplicate state or generating unsustainable Firestore read/write volumes.

### Work and approaches

- Tested Firestore-backed asset storage.
- Introduced map-asset chunking and bounded reads.
- Considered autosave but retained controlled admin saves because of write and conflict risk.
- Investigated VPS/API storage, then reverted after asset persistence and visibility became unreliable.
- Diagnosed duplicate-key and identity problems affecting React rendering.
- Explored viewport-based loading, simplified geometry and separation of large asset groups.

### Evidence required

Performance profiles, asset-count tests, failed API/VPS prototype records, Firestore metrics, commits for chunking/bounded reads, screenshots and defect reports.

## 2. Fibre-network topology and continuity modelling

### Advance sought

A data model and engine capable of representing physical fibre paths from exchange equipment through EBCL, feeder, WDM, splitter, joints, cables and distribution assets, including through-splices and fibre-range continuity.

### Uncertainty

A geographic line-and-point model does not by itself describe optical continuity. It was uncertain how to maintain correct relationships when assets span multiple areas, cables contain hundreds of fibres, fibres are split or spliced, and records are edited independently.

### Work and approaches

- Separated distribution assets from global core/feeder assets.
- Defined exchange equipment and meet-me continuity structures.
- Modelled fibre ranges and direct through-splice relationships.
- Considered graph-based topology and route tracing.
- Developed rules for uniqueness, splitter relationships and cross-area behaviour.

### Evidence required

Topology schemas, continuity spreadsheets, test networks, trace results, failed models, validation rules and commits implementing graph or relationship logic.

## 3. Multi-tenant data isolation and configurable storage

### Advance sought

A single platform capable of supporting multiple companies while keeping organisations, projects, files, assets, permissions and audit records correctly isolated, with future support for different client storage providers.

### Uncertainty

It was uncertain how to provide a consistent application and API while allowing Firebase, Microsoft/Azure or AWS-backed storage options without duplicating business logic or weakening tenant isolation.

### Work and approaches

- Defined business, project, area and membership boundaries.
- Planned organisation-aware API and permission checks.
- Added client storage preference to onboarding requirements.
- Considered a storage abstraction behind platform services.
- Separated test data from employer/client-owned data.

### Evidence required

Tenant-boundary diagrams, Firestore rules, API middleware, storage adapter experiments, penetration/security tests and records of rejected designs.

## 4. Secure API modularisation without breaking the live platform

### Advance sought

Convert the existing application into modular services and APIs while retaining current GIS behaviour, authentication, real-time updates and user workflows.

### Uncertainty

The existing front end, Firebase data model and operational modules were tightly connected. It was unclear how to introduce service boundaries, permissions, versioning and client-hosted options without causing inconsistent data, latency or extensive regressions.

### Work and approaches

- Defined APIs for Map, Projects, Assets, Audits, Workspace, Production, H&S, Topology, Openreach and Files.
- Considered front end -> gateway -> identity/permissions -> service architecture.
- Classified services as active or planned.
- Explored packaging and deployment through GitHub, Vercel and Firebase.

### Evidence required

Architecture decision records, API specifications, migration commits, compatibility tests, latency measurements and records of failed integrations.

## 5. Geospatial import and normalisation

### Advance sought

Reliable ingestion of GeoJSON, KML, KMZ and GPKG data into the AlistraGIS asset model while preserving geometry, coordinates, attribution and usable asset types.

### Uncertainty

Input files can use different coordinate reference systems, geometry types, schemas, nesting and metadata. It was uncertain how to normalise these formats without crashing the map, losing meaning or producing invalid assets.

### Work and approaches

- Used GeoJSON as the initial internal interchange format.
- Identified KML import crashes.
- Added requirements for KML, KMZ and GPKG support.
- Considered validation, conversion, streaming/chunking and rejection reporting.

### Evidence required

Problem files, crash logs, parser prototypes, coordinate tests, import validation reports and before/after datasets.

## 6. Mobile and tablet GIS performance

### Advance sought

A field-usable tablet/mobile implementation that retains critical GIS and operational capabilities without the desktop interface becoming unusable on smaller devices.

### Uncertainty

Complex map controls, drawers, layers and editable geometry did not reliably fit or behave across mobile browsers, landscape mode and touch input. It was unclear whether a separate shell or responsive desktop-parity approach would be more robust.

### Work and approaches

- Prototyped a dedicated mobile shell.
- Reconsidered the design in favour of desktop parity.
- Logged drawer, overlay, login, landscape and control-placement defects.
- Restricted high-risk drawing functions while retaining measure, navigation and layer controls.

### Evidence required

Device matrix, screenshots, browser logs, performance timings, touch interaction tests and implementation comparisons.

## 7. Audit integrity, session control and high-volume logging

### Advance sought

Secure, useful audit and session controls that preserve evidence without generating excessive writes or allowing users to forge/delete history.

### Uncertainty

Two separate asset-view logging paths created uncapped writes, while general Firestore rules risked allowing change-log manipulation. It was uncertain how to enforce append-only, server-stamped logs and concurrent-seat controls without harming responsiveness.

### Work and approaches

- Identified duplicate view logging.
- Planned debouncing/aggregation for frequent view events.
- Reviewed server-side callable functions for change logging.
- Planned rule exclusions and immutable audit collections.
- Defined a one-active-session-per-paid-seat requirement.

### Evidence required

Security audit findings, Firestore rules, Cloud Function code, load tests, session race-condition tests and remediation commits.

## 8. AI-assisted network engineering

### Advance sought

Automated assistance capable of analysing a proposed build area, drawing a feasible fibre network, allocating fibres and preserving spare capacity according to engineering rules.

### Uncertainty

It was unclear whether general AI models could reliably satisfy hard geospatial, capacity, topology and constructability constraints. The likely uncertainty lies in combining deterministic engineering rules, graph optimisation and AI-generated proposals with validation.

### Work and approaches

- Defined the FRIDAY AI concept.
- Considered code scanning and defect identification.
- Explored polygon-based auto-design and spare-fibre constraints.
- Recognised the need for deterministic validation rather than relying solely on model output.

### Evidence required

Prototype algorithms, prompts and outputs, validation failures, benchmark designs, constraint definitions and human-review results.

## Activities likely outside the R&D boundary

Unless directly tied to resolving one of the above uncertainties, the following are generally expected to be non-qualifying or only partly qualifying:

- routine UI restyling and visual mock-ups;
- marketing websites and sales materials;
- commercial pricing and licensing discussions;
- normal customer onboarding;
- routine maintenance, content entry and straightforward bug fixes;
- legal, accounting and GDPR documentation not directly supporting technological work.
