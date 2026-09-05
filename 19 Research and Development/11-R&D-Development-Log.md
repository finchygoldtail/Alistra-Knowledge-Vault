# AlistraGIS R&D Development Log

Use one entry for each meaningful technical investigation. Add links to commits, screenshots, test files and invoices wherever possible.

---

## Entry template

### Date / period

YYYY-MM-DD or date range

### Project area

Map / Topology / API / Import / Mobile / Security / Other

### People involved

Names, roles and whether employee, director or contractor.

### Technical objective

What capability were we attempting to achieve?

### Baseline

What existing technology, libraries, documentation or standard approach was available?

### Technological uncertainty

Why could a competent professional not readily determine the solution in advance?

### Work performed

- Experiments and prototypes
- Code or configuration changed
- Tests completed
- Alternatives considered

### Failures or unexpected results

Record crashes, incorrect output, scaling failures, data corruption, security concerns or rejected designs.

### Outcome

What was learned or achieved? Is the uncertainty resolved, partly resolved or still open?

### Evidence links

- Git commit / PR:
- Deployment:
- Screenshot / video:
- Test data:
- Issue / audit:
- Invoice or cost record:

### Time allocation

- Total hours:
- Estimated qualifying R&D hours:
- Non-R&D hours:
- Basis for estimate:

---

## Initial reconstructed entry — map performance and storage

### Date / period

Pre-incorporation through July 2026; exact dates to confirm from Git history.

### Project area

Map and data storage.

### Technical objective

Keep the browser-based GIS responsive while loading, editing and synchronising increasing numbers of fibre assets.

### Technological uncertainty

The application experienced slowdown as asset numbers increased. It was unclear how to combine real-time Firestore updates, map rendering, editable geometry and controlled database usage without loading excessive data or creating conflicting state.

### Work performed

- Used Firestore-backed map assets.
- Introduced asset chunking and bounded-read concepts.
- Considered autosave and retained controlled admin saves because of write-volume concerns.
- Tested a VPS/API storage route.
- Reverted to Firestore when asset saving and immediate visibility were unreliable.
- Investigated duplicate React keys and asset identity issues.

### Outcome

The uncertainty remains partly open. Firestore remains the working storage platform, while viewport loading, service APIs and larger-scale testing require further evidence.

### Evidence links

To add: commits, performance logs, screenshots, Firestore usage metrics and records from the VPS/API attempt.

---

## Initial reconstructed entry — multi-format geospatial import

### Date / period

July 2026; exact dates to confirm.

### Project area

Geospatial import.

### Technical objective

Import industry-standard KML, KMZ and GPKG files alongside GeoJSON without crashing the map or producing invalid assets.

### Technological uncertainty

Different formats can contain incompatible schemas, coordinate systems, geometry types and large datasets. A KML import was reported to crash the map, showing that straightforward loading was insufficient.

### Work performed

- Retained GeoJSON as the initial working interchange format.
- Added requirements for KML, KMZ and GPKG support.
- Identified the need for validation, conversion, chunking and clear rejection reporting.

### Outcome

Still open. Test files, crash logs and import benchmarks must be collected before the technical solution can be evidenced.
