# AlistraGIS R&D Risk Register

> Purpose: track technical, evidence, cost and claim-preparation risks associated with AlistraGIS research and development work.

## Scoring

- **Likelihood:** 1 Rare, 2 Unlikely, 3 Possible, 4 Likely, 5 Almost certain
- **Impact:** 1 Minor, 2 Moderate, 3 Significant, 4 Major, 5 Critical
- **Score:** Likelihood × Impact
- **Priority:** 1–4 Low, 5–9 Medium, 10–16 High, 17–25 Critical

## Register

| ID | Risk | Category | Likelihood | Impact | Score | Priority | Mitigation / control | Owner | Status |
|---|---|---|---:|---:|---:|---|---|---|---|
| RND-R01 | Historic R&D work cannot be reconstructed with reliable dates, decisions and evidence | Evidence | 4 | 5 | 20 | Critical | Backfill journal from Git history, deployments, conversations, screenshots and invoices; record future work contemporaneously | Alistair | Open |
| RND-R02 | Routine product development is mixed with work resolving technological uncertainty | Claim scope | 4 | 5 | 20 | Critical | Tag journal entries and costs by innovation ID; explicitly record routine work excluded | Alistair / adviser | Open |
| RND-R03 | Time spent by the director/developer is not supported by credible records | Cost evidence | 4 | 5 | 20 | Critical | Start monthly time records; reconcile to commits, calendar and journal entries; document allocation method | Alistair | Open |
| RND-R04 | Pre-incorporation work is incorrectly included in the company claim | Tax boundary | 3 | 5 | 15 | High | Establish incorporation date, contracting entity and payment source; obtain accountant advice before inclusion | Accountant | Open |
| RND-R05 | Cloud, AI-tool and software costs are claimed without separating development, testing, live use and general business use | Cost allocation | 4 | 4 | 16 | High | Export monthly billing; define allocation keys; retain calculations and invoices | Alistair / accountant | Open |
| RND-R06 | Claimed technological baseline is not researched or documented | Technical narrative | 3 | 5 | 15 | High | Add baseline references and alternatives considered to every detailed innovation record | Technical lead | Open |
| RND-R07 | The claimed advance is described as a product feature rather than an advance in technology | Technical narrative | 4 | 5 | 20 | Critical | Frame each project around capability, uncertainty, experimentation and resolution; obtain competent-professional review | Technical lead / adviser | Open |
| RND-R08 | Source-control evidence contains customer or employer-owned information that should not be used | Data/IP | 3 | 5 | 15 | High | Use test/synthetic data; redact confidential details; maintain evidence index without copying restricted datasets | Alistair | Open |
| RND-R09 | Public repository exposes confidential commercial, security or personal information | Security | 3 | 5 | 15 | High | Review repository visibility and contents; never store secrets, credentials, personal data or exploitable security details | Alistair | Open |
| RND-R10 | Large GIS datasets cause browser freezes, crashes or unacceptable field performance | Technical | 4 | 4 | 16 | High | Define performance budgets; create representative datasets; test bounded reads, chunking, clustering and worker-based processing | Engineering | Active |
| RND-R11 | Real-time edits produce stale state, conflicts or asset loss | Technical | 3 | 5 | 15 | High | Add revisions, conflict handling, transactional tests, recovery and audit history | Engineering | Active |
| RND-R12 | Fibre topology model gives incorrect continuity or capacity results | Technical | 3 | 5 | 15 | High | Build golden test networks; verify traces fibre-by-fibre; preserve manual override and audit history | Engineering / fibre SME | Active |
| RND-R13 | KML, KMZ or GPKG imports crash the map or silently corrupt geometry | Technical | 4 | 4 | 16 | High | Validate before import; process in stages; cap size; test projections and malformed fixtures; provide rollback | Engineering | Active |
| RND-R14 | Multi-tenant permissions allow cross-company or cross-project data access | Security / technical | 3 | 5 | 15 | High | Automated rules/API tests, least privilege, server-side tenant checks and adversarial review | Engineering | Active |
| RND-R15 | Audit logs can be forged, altered, deleted or duplicated | Security / evidence | 4 | 5 | 20 | Critical | Restrict direct writes; stamp server-side; make history append-only; deduplicate events; test rules | Engineering | Active |
| RND-R16 | View and activity logging produces uncontrolled database writes and cost | Technical / cost | 4 | 4 | 16 | High | Debounce or aggregate non-critical events; define retention; monitor writes per user and action | Engineering | Active |
| RND-R17 | Mobile/tablet interface is unusable or permits unauthorised map edits | Technical / operational | 3 | 4 | 12 | High | Device matrix, permission tests, simplified field controls and landscape/portrait testing | Engineering / field users | Active |
| RND-R18 | Client-selectable storage adapters behave inconsistently across Firebase, Microsoft and AWS | Technical | 4 | 5 | 20 | Critical | Define provider-neutral contracts; capability matrix; conformance tests; phased prototype before commitment | Architecture | Candidate |
| RND-R19 | API decomposition creates inconsistent authorisation or partial updates across services | Technical | 3 | 5 | 15 | High | Gateway enforcement, idempotency, versioned contracts, integration tests and compensation/retry design | Architecture | Active |
| RND-R20 | Evidence files, screenshots or test outputs are later lost or cannot be linked to the relevant work | Evidence | 3 | 4 | 12 | High | Use stable evidence IDs, checksums where appropriate, repository links and monthly evidence review | Alistair | Open |
| RND-R21 | R&D narrative or costs are prepared too late for a proper review before filing | Governance | 3 | 4 | 12 | High | Quarterly review and year-end readiness checkpoint; appoint accountant/adviser early | Alistair | Open |

## Highest-priority actions

1. Start contemporaneous time, cost and engineering records immediately.
2. Backfill historical work using objective evidence and mark any uncertain dates clearly.
3. Separate routine implementation from technological uncertainty.
4. Review repository confidentiality and ensure no secrets or restricted customer/employer data are stored.
5. Build repeatable tests for performance, topology, imports, permissions and audit logs.
6. Confirm pre-incorporation and cost-eligibility treatment with an accountant or R&D adviser.

## Risk review template

### RND-RXX — Risk title

- **Date identified:**
- **Linked innovation IDs:**
- **Description:**
- **Cause:**
- **Potential consequence:**
- **Current controls:**
- **Planned actions:**
- **Action owner:**
- **Target date:**
- **Residual likelihood:**
- **Residual impact:**
- **Evidence of closure:**

## Review cycle

- Review active technical risks during engineering planning.
- Review evidence and cost risks monthly.
- Review claim-boundary and adviser questions quarterly.
- Close a risk only when supporting evidence is linked.