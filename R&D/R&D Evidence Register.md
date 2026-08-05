# AlistraGIS R&D Evidence Register

> Purpose: maintain an indexed chain of evidence showing what technical work was performed, when it happened, who was involved, what uncertainty it addressed and what was learned.

## Evidence rules

- Use one stable evidence ID per item or evidence bundle.
- Keep the original date, author and source wherever possible.
- Link evidence to an Innovation Register ID and Engineering Journal entry.
- Do not store passwords, API keys, private customer data, personal data or employer-owned network data.
- Use synthetic or redacted examples when evidence contains restricted information.
- Record limitations honestly; do not reconstruct certainty that the source does not support.

## Evidence register

| Evidence ID | Date / period | Type | Description | Innovation IDs | Location / reference | What it demonstrates | Confidentiality | Review status |
|---|---|---|---|---|---|---|---|---|
| EVD-001 | 2026-08-05 | Governance record | R&D Engineering Journal, Costs, Innovation Register, Risk Register and Evidence Register established | All | `R&D/` folder in this repository | Start of structured contemporaneous R&D record keeping | Internal | Added |

## Evidence categories

### Source control

Useful evidence includes:

- Commits and pull requests
- Branch names and timestamps
- Code diffs showing prototypes, failed approaches and architectural changes
- Issue discussions and review comments
- Test fixtures and automated test results
- Release tags and deployment references

| Evidence ID | Commit / PR | Date | Summary | Innovation ID | Journal link | Notes |
|---|---|---|---|---|---|---|
| | | | | | | |

### Technical conversations and design records

Potential sources:

- ChatGPT and Codex development conversations
- Architecture handovers
- Technical decision records
- Diagrams and data-model drafts
- Design comparisons and rejected approaches

For each conversation, preserve the date, relevant extract or export, and a short explanation of the engineering decision it supports. Avoid relying on a large unfiltered conversation dump without an index.

| Evidence ID | Date | Conversation / record | Decision or uncertainty | Innovation ID | Stored location | Notes |
|---|---|---|---|---|---|---|
| | | | | | | |

### Tests and experiments

Examples:

- Asset-volume and map-rendering benchmarks
- Database read/write counts
- Import tests for KML, KMZ, GPKG and GeoJSON
- Topology trace and capacity validation
- Permission and cross-tenant access tests
- Mobile/tablet device testing
- Offline, latency and failure-recovery tests
- Audit-log immutability and duplication tests

| Evidence ID | Test date | Test name | Dataset / environment | Expected result | Actual result | Innovation ID | Test file / output |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

### Screenshots, renders and recordings

Capture evidence showing:

- Broken or incomplete states before technical work
- Prototype behaviour
- Performance or device failures
- Successful implementation after testing
- Developer console errors where relevant
- Field workflow behaviour on actual devices

| Evidence ID | Date | Image / recording | Before / after | Innovation ID | Location | Explanation |
|---|---|---|---|---|---|---|
| | | | | | | |

### Deployments and runtime records

Potential sources:

- Vercel deployment logs
- Firebase / Google Cloud logs
- Error reports
- Performance monitoring
- Database usage reports
- Security alerts and traffic reports

| Evidence ID | Date | Environment | Deployment / log reference | Innovation ID | Finding | Follow-up |
|---|---|---|---|---|---|---|
| | | | | | | |

### Cost and time evidence

Potential sources:

- Payroll and director remuneration records
- Monthly time records
- Supplier invoices
- Cloud billing exports
- AI development-tool invoices
- Subcontractor agreements and invoices
- Allocation calculations

| Evidence ID | Period | Evidence type | Supplier / person | Amount / hours | Cost register link | Stored location | Review status |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

## Initial historical evidence collection list

The following sources should be collected and indexed:

1. GitHub commit history for the AlistraGIS application and related repositories.
2. Vercel deployment history and build logs.
3. Firebase configuration, rules history, emulator tests, billing and usage reports.
4. ChatGPT/Codex conversations covering architecture, defects, experiments and implementation decisions.
5. Existing UI renders and device screenshots.
6. Console errors and audit findings, including duplicate keys, import crashes, uncontrolled view logs and change-log security concerns.
7. KML/KMZ/GPKG/GeoJSON sample files and conversion outcomes using synthetic or authorised data.
8. Topology examples for EBCL, feeders, WDMs, splitters, LMJs, joints and DPs using non-confidential test identifiers.
9. Mobile and tablet test records across representative devices and orientations.
10. Invoices and billing reports for development tools, cloud services and mapping services.
11. Records showing when AlistraGIS was incorporated and which entity incurred each cost.
12. Competent-professional notes explaining the baseline, uncertainties and outcomes.

## Evidence bundle template

### EVD-XXX — Evidence title

- **Evidence date / period:**
- **Collected on:**
- **Author / source:**
- **Evidence type:**
- **Linked innovation IDs:**
- **Linked journal entries:**
- **Linked cost entries:**
- **Repository / storage location:**
- **Description:**
- **What it proves:**
- **Known limitations:**
- **Confidentiality classification:** Public / Internal / Confidential / Restricted
- **Redaction required:** Yes / No
- **Reviewed by:**
- **Review date:**

## Monthly evidence review

- Confirm every active innovation has recent evidence.
- Check that journal claims are supported by objective records.
- Link costs and time entries to technical activities.
- Preserve failures and abandoned approaches, not only successful outcomes.
- Check that restricted data and secrets have not been committed.
- Verify links still work and exported evidence has been backed up.
- Identify gaps requiring explanation or further testing.

## Evidence quality scale

- **Strong:** dated, objective, directly linked and independently verifiable
- **Moderate:** dated and relevant but requires explanation or allocation
- **Weak:** recollection, undated note or unsupported estimate
- **Not usable:** unverifiable, restricted, misleading or unrelated

## Important note

Evidence should support an accurate technical narrative; it should not be altered or selectively presented to create a misleading claim. Any uncertainty or gap should be recorded openly and reviewed with the claim adviser.