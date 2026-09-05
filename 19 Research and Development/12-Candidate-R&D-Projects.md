# Candidate AlistraGIS R&D Project Register

This register groups development into possible claim projects. The final structure should follow the accounting period and HMRC requirements rather than simply mirroring product modules.

## Project A — Scalable browser-based fibre GIS

**Status:** Active / partly resolved

**Advance sought:** A responsive, multi-user browser GIS for large, editable fibre-network datasets.

**Primary uncertainties:** Rendering scale, query boundaries, synchronisation, geometry editing, asset identity and database read/write control.

**Known evidence:** Firestore architecture, chunking approach, bounded-read plans, autosave decision, performance problems, VPS/API experiment and React duplicate-key defects.

**Next evidence:** Benchmark repeatable asset counts and measure load time, interaction latency, memory use, Firestore reads and writes.

## Project B — Fibre topology and optical continuity engine

**Status:** Active / early development

**Advance sought:** End-to-end modelling and tracing of fibre connectivity across exchanges, cables, splitters, joints and distribution assets.

**Primary uncertainties:** Graph structure, fibre-range mapping, split/merge relationships, cross-area assets, validation and trace consistency after edits.

**Known evidence:** EBCL/feeder structures, meet-me continuity, 240-fibre records, WDM and splitter modelling, distribution/core separation.

**Next evidence:** Create benchmark topologies with known expected traces and document failed relationship models.

## Project C — Multi-tenant API and storage abstraction

**Status:** Planned / active architecture work

**Advance sought:** Secure organisation-separated services with configurable client storage while maintaining one consistent platform.

**Primary uncertainties:** Tenant boundary enforcement, storage-provider abstraction, permission propagation, performance and migration from direct Firebase coupling.

**Known evidence:** API catalogue, organisation/project model, storage preference requirement and front-end/gateway/service architecture.

**Next evidence:** Build and compare at least two storage adapters; test cross-tenant access and failure behaviour.

## Project D — Geospatial ingestion pipeline

**Status:** Open

**Advance sought:** Reliable ingestion and normalisation of GeoJSON, KML, KMZ and GPKG.

**Primary uncertainties:** Coordinate systems, geometry variation, schemas, file size, conversion accuracy and browser stability.

**Known evidence:** GeoJSON implementation, KML crash report and multi-format requirement.

**Next evidence:** Assemble representative files, define expected outputs and run repeatable conversion/performance tests.

## Project E — Field-ready tablet and mobile GIS

**Status:** Active / partly resolved

**Advance sought:** Preserve critical mapping and operational capability on touch devices without maintaining an entirely separate product.

**Primary uncertainties:** Responsive layout, map interaction, drawer behaviour, landscape mode, touch editing and acceptable performance.

**Known evidence:** Mobile-shell investigation, decision to pursue desktop parity, tablet screenshots and defect list.

**Next evidence:** Formal device/browser matrix and task-based field tests.

## Project F — Secure audit and licensed-session control

**Status:** Active remediation

**Advance sought:** Tamper-resistant, scalable audit history and one-active-session controls compatible with Firebase authentication and real-time use.

**Primary uncertainties:** Server-only audit stamping, immutable logs, write amplification, race conditions and session revocation.

**Known evidence:** Security audit findings, duplicate view logs, callable function and Firestore-rule concerns, concurrent-seat requirement.

**Next evidence:** Load and race-condition testing, rule tests and evidence that clients cannot alter audit records.

## Project G — AI-assisted fibre design and quality analysis

**Status:** Research concept

**Advance sought:** Use AI with deterministic engineering constraints to propose or review fibre-network designs and identify defects.

**Primary uncertainties:** Reliability of model output, constraint satisfaction, topology validation, explainability and safe integration with live data.

**Known evidence:** FRIDAY concept, code-scanning requirement, polygon auto-design idea and spare-fibre rule.

**Next evidence:** Define a limited benchmark, expected engineering constraints and measurable acceptance criteria before development.

## Claim-priority view

The strongest initial candidates appear to be Projects A and B because they involve the core technical platform and have identifiable uncertainties. Projects C, D and F may become strong as prototypes and tests are produced. Project E needs evidence that the work extended beyond ordinary responsive design. Project G should not be claimed merely for integrating an existing AI service; evidence would need to show genuine technological uncertainty and systematic experimentation.
