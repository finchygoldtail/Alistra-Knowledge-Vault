# AlistraGIS GitHub Development Evidence Timeline

> Purpose: reconstruct AlistraGIS development activity from source-control evidence. Commit timestamps prove that development activity occurred at those times; they do **not** by themselves prove continuous working hours between commits. Use this record alongside contemporaneous user time records, AI usage records, CI/build logs and invoices before calculating labour cost or any R&D claim.

## Evidence method

- Source repository: `finchygoldtail/AlistraGIS`
- Primary evidence: commit timestamps and commit descriptions.
- Time zone: GitHub timestamps reviewed in UK local time where exposed by the connector.
- A first-to-last commit span is an **activity window**, not automatically paid/claimable hours.
- Where Alistair has made a contemporaneous statement of hours, that statement is recorded separately in the AI and Development Cost Register.
- Routine feature work, ordinary bug fixing and commercial/product design must be distinguished from work addressing technological uncertainty before R&D treatment is finalised.

## Key development origin — duct and sub-duct workflow

### 2026-07-22

**18:10 — `73fd9b47` — Add duct and sub-duct route workflow**

Major new functionality introduced duct as a mapped LineString asset with duct count, diameter and use; linked cables to selected ducts; and added generation of child sub-duct records along the duct geometry.

**18:33 — `7527ff13` — Separate duct storage and layers**

Follow-on architecture separated duct storage/layer handling.

**Evidence interpretation:** source control shows the duct/sub-duct development stream was active by 22 July 2026. The two duct commits span at least 23 minutes of visible commit activity, but actual design/implementation/test time before the first commit is not inferable from timestamps alone.

### 2026-07-23

Duct development continued across an evidenced commit window from approximately **15:58 to 19:39**, including:

- `7b6cd4c5` — Add duct designer and route visibility
- `a9c633d2` — Add ducts to workspace layer menu
- `7fd5a7e4` — Fix workspace duct layer count
- `1ab5a225` — Keep workspace ducts visible at overview zoom
- `99a484fa` — Fix duct clicks and polygon edit locking
- `cbdab084` — Open duct editor from workspace asset details
- `b8e5d2ab` — Forward workspace duct editor action

**Evidence interpretation:** at least 3 hours 40 minutes elapsed between the first and last identified duct-related commits. This is evidence of sustained activity, not a claim that every minute was working time.

### 2026-07-24

A concentrated duct/cable containment development run is evidenced from approximately **14:07 to 18:45**, including:

- Keep ducts visible while drawing cables
- Show assigned cables in duct editor
- Route duct-assigned cables along duct geometry
- Improve duct usage render
- Keep duct-linked cables synced to duct route
- Select duct containment path when drawing cables
- Render cables in leaf sub-duct paths
- Separate nested duct render positions
- Show cable names in sub-duct schedule
- Reconcile cables into child sub-ducts
- Add duct zoom and capacity warning
- Keep design ducts and cables visible

**Evidence interpretation:** this is a strong source-control trail for the technical development of hierarchical duct/sub-duct containment, visualisation and cable routing. The visible commit window spans about 4 hours 38 minutes; actual work may have started before the first commit or continued between/after commits.

### 2026-07-27 and 2026-07-29

Further duct work continued:

- `f43daafe` — Count ducts in asset register
- `982040f0` — Scope duct cables and split routes at joints

These commits demonstrate the duct model continued to be integrated into asset counting and topology/route splitting rather than ending with the initial July implementation.

---

## 2026-08-02 to 2026-08-03 — duct progress, route splitting, field/mobile and network integration

Late on 2 August and into 3 August, GitHub shows continued work on:

- Completed-sections layer and duct progress
- Workspace duct visibility/selection/deployment fixes
- Individual duct rendering and size colours
- Repeated-vertex route splitting
- Duct joint insertion from route popups
- Coordinate normalisation and invalid-route guards
- Mobile duct workflows
- QGIS export metadata
- Splitting linked ducts when adding joints
- Mobile production classification fixes
- Network schematic work
- Tablet and phone field-workspace improvements
- Audit photo/camera workflows
- Joint photos
- Universal map popup navigation and camera capture

The 3 August repository history shows development activity across much of the day, with commits from around midday through late evening plus route work around midnight. Do not convert the raw first/last timestamp directly into hours without reconciling breaks and off-screen design/testing time.

---

## 2026-08-04 — reliability, data-loss, performance, KML and security hardening

Major evidenced work included:

- Targeted per-asset saving to prevent silent field/photo/edit data loss
- Reduced Firestore write volume by avoiding whole-project rewrites
- Photo cleanup/compression and Storage cost reductions
- Home-save reliability improvements
- Exchange incremental writes
- Viewport culling and map performance improvements
- KML multi-point/folder-path import fixes
- Cable snap throttling
- Audit logging duplication/cost reductions
- Resumable uploads and persistent failed-upload retry queues
- Audit trail server-managed write hardening

This period is particularly relevant when separating routine bug fixing from deeper technical work on data integrity, offline/field reliability, write-volume control and audit immutability.

---

## 2026-08-05 — large-scale refactoring, security, ticketing and workspace wiring

GitHub shows a very large structural refactor across core application files and associated reliability/security work.

Examples include:

- JointMapManager extraction rounds
- ProjectWorkspace extraction rounds
- UserManagementPanel extraction
- DistributionPointEditor extraction
- WorkspaceBuild extraction
- ExchangeDesigner extraction
- WorkspaceMap extraction
- AssetMarkersLayer extraction
- StreetCabDesigner extraction
- `useJointMapWorkspaceHandlers` extraction
- Map canvas/side panel/control overlay context memoisation work
- Internal ticketing/helpdesk system
- High-severity audit fixes
- Map-asset permission hardening
- Dead workspace tab wiring
- TDZ/runtime crash fixes

A key refactor commit, `9739be4d`, reduced `JointMapManager.tsx` from 4,077 to 2,875 lines and extracted the autosave, pending-save recovery, context-add handling, duct-joint insertion and the approximately 527-line duct/sub-duct/cable creation workflow into dedicated modules.

**Evidence interpretation:** the source-control trail supports the user's statement that substantial time has been spent refactoring buggy/entangled code. Exact labour hours must still be reconstructed rather than inferred from commit count.

---

## 2026-08-06 — map render refactoring, security hardening, QA fixes and new operational modules

Evidenced activity included:

- Completion of map side-panel/control-overlay memoisation
- Ticket callable hardening
- Lifecycle/QA/report UI corrections
- Keyless CARTO basemap replacement after MapTiler key failure
- QA issue selection/resolve repair
- Plant & Equipment module
- Vehicle Management module
- Smart Work Pack extensions
- Crew register and shared documents model

The major commit `cd8ca13f` added company-wide Plant & Equipment and Vehicle registers with check-in/out, fault reporting, inspections/services/calibration, compliance alerts, CSV export, QR labels, camera/manual checkout, Excel bulk import, shared crews/documents and additive Work Pack lifecycle/readiness functionality. The commit records 151 passing unit tests and clean typecheck/build on both sides.

---

## 2026-08-07 — vehicles, equipment, employees, licensing/session controls and audit fixes

### Contemporaneous user time record

Alistair recorded starting work at **09:00** and working through the day on vehicles, equipment and employees implementation, with extensive refactoring/debugging. The AI and Development Cost Register currently records a 10.5-hour elapsed window to approximately 19:30, pending break reconciliation.

### GitHub evidence

Source control independently shows commits during the day including:

- `4626201e` — Supervisor role, single-session enforcement, employee credentials, vehicle QR scan, Crews toggle, Fleet tab and as-built generator
- `d7846626` — Module entitlement filtering in map layers
- `2bcee223` — User Register scrolling/selection fix
- `d46fd53f` — Active Users KPI wiring
- `ab965ab5` — Move Plant Equipment, Vehicles and Employees into Management
- `905c8e96` — Batch imports and document-storage security fix
- `1090e918` — Employee KPI leak fix and shared Plant/Vehicle/Employee toolbar styling
- `39f91285` — Six further Round 4 audit findings fixed
- `125262ad` — Final Round 4 session-stamp findings closed

The GitHub commits provide independent evidence that the day included both new product capability and defect/security/refactor work, not only planning.

---

## Development workstreams evidenced since duct/sub-duct creation

1. Duct/sub-duct route and hierarchy modelling
2. Cable containment and duct-slot routing
3. Duct/joint route splitting and topology behaviour
4. Production/progress integration
5. QGIS/KML/import-export handling
6. Mobile/tablet field workflows
7. Asset photo/evidence capture and upload reliability
8. Firestore write-volume and data-loss prevention
9. Map rendering/performance and context memoisation
10. Large core-file refactoring and module extraction
11. Audit-trail/security/permission hardening
12. Ticketing/helpdesk
13. Plant and equipment management
14. Vehicle/fleet management
15. Employees, credentials, supervisors and seat/session controls
16. Crew management
17. Smart Work Pack lifecycle/readiness
18. Commercial GIS / takeoff / recipe / stock / package API design (design evidence currently in the R&D journal; implementation commits to follow)

## Time-reconstruction rule

For accounting/R&D evidence, use a hierarchy of confidence:

1. **Highest confidence:** contemporaneous start/finish/break record supplied by Alistair.
2. **High confidence:** AI coding session usage plus GitHub commit/CI timestamps that align to the same workstream.
3. **Supporting evidence:** first/last commit windows and dense commit clusters.
4. **Do not use alone:** number of commits multiplied by an assumed time-per-commit.

Git commits should therefore support and corroborate a time record, not manufacture one.

## Next evidence actions

- Export Claude/Claude Code usage history and receipts where available.
- Export OpenAI/Codex paid-credit/API usage where applicable.
- Link relevant Vercel deployments and CI/build runs to major development days.
- Reconstruct Jul 22 onward working sessions where sufficient evidence exists.
- Add actual break-adjusted hours when remembered or supported.
- Mark each work block as technical R&D, qualifying indirect work, routine product development, commercial/admin, or uncertain/adviser-review.
