# AlistraGIS R&D Innovation Register

> Purpose: identify the advances AlistraGIS is attempting, the technological baseline, the uncertainties encountered and the work undertaken to resolve them.

## Assessment scale

- **Candidate:** potentially relevant but not yet evidenced
- **Active R&D:** a technological uncertainty is currently being investigated
- **Resolved:** the uncertainty has been overcome and evidence is available
- **Abandoned:** the attempted approach did not work or was not commercially/technically viable
- **Routine:** implementation using readily available knowledge; normally not treated as R&D

## Innovation register

| ID | Innovation / workstream | Baseline technology | Proposed advance | Key technological uncertainty | Status | Evidence needed |
|---|---|---|---|---|---|---|
| INN-001 | Large-scale interactive telecom GIS | Standard browser mapping libraries and cloud document databases | Maintain responsive editing, bounded loading and real-time collaboration across large fibre asset datasets | How to partition, load, synchronise and persist interrelated geometry without freezes, stale edits or excessive writes | Active R&D | Performance tests, architecture decisions, commits, failed approaches |
| INN-002 | Fibre-network topology and continuity engine | Generic GIS features and relational/graph concepts | Model fibre-by-fibre continuity through exchanges, feeders, joints, splitters, DPs and meet-me locations | How to preserve physical and logical continuity, capacity and audit history while assets are edited spatially | Active R&D | Data models, test networks, trace results, topology defects and fixes |
| INN-003 | Multi-tenant operational GIS architecture | Firebase authentication, Firestore rules and conventional SaaS tenancy | Enforce company, project, area, role and storage boundaries consistently across map, workspace and API services | How to prevent cross-tenant leakage while supporting shared/global network assets and delegated permissions | Active R&D | Rule tests, threat models, tenancy tests, permission matrices |
| INN-004 | Multi-format geospatial normalisation | Existing KML, KMZ, GeoJSON and GPKG parsers | Import telecom datasets into one controlled internal model without geometry or attribute loss | How to handle projections, malformed files, large datasets, nested KML and unsupported attributes safely | Active R&D | Import fixtures, conversion logs, crash reproductions, validation results |
| INN-005 | Field-capable tablet/mobile GIS | Responsive web layouts and mobile map controls | Provide a reduced field workflow with map parity, evidence capture and strict draw/edit permissions | How to retain usability and spatial accuracy on constrained screens and intermittent connections | Active R&D | Device tests, screenshots, interaction defects, offline/poor-network tests |
| INN-006 | Client-selectable data storage | Single-provider Firebase architecture | Allow customer data to reside in Firebase, Microsoft or AWS-backed storage while preserving one application/API contract | How to abstract storage without inconsistent permissions, transactions, search, evidence or audit behaviour | Candidate | Architecture spikes, provider comparison, adapter prototypes |
| INN-007 | Auditable asset history at sustainable write volume | Direct client writes and event logs | Produce trustworthy server-stamped change history while avoiding duplicated or uncapped view events | How to guarantee immutability and completeness without excessive cost or performance impact | Active R&D | Security audit, write metrics, rules tests, revised logging design |
| INN-008 | API decomposition of the GIS platform | Monolithic React/Firebase application patterns | Separate map, assets, projects, production, audits, H&S, files and topology into protected service contracts | How to preserve consistency and authorisation across independently evolving modules | Active R&D | API catalogue, contracts, gateway design, integration tests |
| INN-009 | Assisted telecom network design | Manual planner-led GIS drafting | Generate or recommend network layouts within constraints such as capacity, spare fibres and asset rules | How to convert engineering constraints into valid, explainable and editable network designs | Candidate | Constraint model, prototype outputs, planner comparison, failure cases |
| INN-010 | Integrated operational project workspace | Separate forms, spreadsheets, maps and field evidence systems | Connect design, production, PIA, QA, commercial, H&S and handover records to the same spatial assets | Whether cross-module state can remain consistent, performant and auditable as workflows progress | Active R&D | Workflow models, state-transition tests, integration defects |

## Detailed innovation record template

### INN-XXX — Title

**Status:**  
**Start date:**  
**Resolution / abandonment date:**  
**Competent professionals involved:**  

**Technological field**  

**Baseline available at the start**  
Describe the publicly available knowledge, products, frameworks and standard techniques considered.

**Advance sought**  
Describe the improvement in overall technological capability, not merely the commercial feature.

**Uncertainties**  
Explain why the method or outcome was not readily deducible.

**Approaches attempted**  
Include failed, partial and superseded approaches.

**Tests and results**  

**Resolution**  
Explain how the uncertainty was resolved, or why it remains unresolved.

**Routine work excluded**  
List styling, content entry, ordinary configuration, bug fixing or commercial work that did not address the uncertainty.

**Linked records**  
- Engineering journal:
- Risks:
- Evidence:
- Costs:
- Source-control references:

## Review guidance

Each candidate should be challenged with these questions:

1. Is the sought advance technological rather than only commercial or user-experience based?
2. Was the baseline researched and recorded?
3. Could a competent professional readily determine the solution at the outset?
4. Is there evidence of systematic investigation or experimentation?
5. Can the start and end of the uncertainty be identified?
6. Can routine implementation be separated from qualifying work?

## Important note

Inclusion in this register does not by itself make an activity eligible for R&D tax relief. The final project boundaries and advance/uncertainty descriptions should be reviewed by a suitably experienced adviser.