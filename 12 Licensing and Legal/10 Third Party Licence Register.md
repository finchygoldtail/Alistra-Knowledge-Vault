---
status: live
updated: 2026-09-05
related: ["[[Decision Log]]", "[[Intellectual Property]]", "[[11 THIRD_PARTY_NOTICES]]"]
---

# Third Party Licence Register

Stage 7 of the commercial go-live programme. Full automated dependency inventory generated with [license-checker-rseidelsohn](https://www.npmjs.com/package/license-checker-rseidelsohn) against fibre-gis's frontend (644 packages including dev/test tooling, 382 production/runtime-shipped) and Cloud Functions dependency trees, re-run 2026-09-05 (originally 2026-08-08, 579 packages — the growth is mainly Turf's per-function submodules and the Vitest/testing-library toolchain, both already covered under existing group entries, not new individually-reviewed risk). AlistraGIS's `map-frontend` has a near-identical dependency set (diffed directly — same runtime dependencies, only test tooling differs), so it is not separately re-audited; treat findings here as applying to both.

**License breakdown (frontend, 579 packages):** 447 MIT, 83 Apache-2.0, 56 ISC, 26 BSD-3-Clause, 11 BSD-2-Clause, plus small counts of MIT-0, Unlicense, 0BSD, BlueOak-1.0.0, CC0-1.0 (all standard permissive) — and 13 packages needing individual review, listed below. No automated removal was done based on licence name alone, per programme rule; each item below was read directly (LICENSE file and/or package.json) rather than trusted to the automated classifier label.

## Needs human/legal review before commercial go-live

| Package | Version | Licence | Where used | Why it needs review |
|---|---|---|---|---|
| **`leaflet-rotate`** | 0.2.8 | **GPL-3.0** (confirmed — read the actual LICENSE file, plain GPLv3, no linking exception) | Direct dependency, adds map-rotation support to Leaflet; shipped in the client bundle | This is the one genuine strong-copyleft dependency found. GPL's copyleft obligations are triggered by *distribution*; whether serving GPL'd JavaScript to a browser as part of a web app counts as "distribution" requiring the combined work's source to be made available is a genuinely debated point in software licensing (unlike AGPL, which explicitly closes this "SaaS loophole" — this is plain GPL-3.0, not AGPL). **This needs an actual solicitor's opinion, not an engineering judgement call** — flagging per programme rule rather than removing or replacing it myself. If legal advises against it, alternatives exist (other rotation plugins, or reimplementing just the rotation feature) but that's a product decision for after the legal read. |
| **`react-leaflet`** (5.0.0) and **`@react-leaflet/core`** (3.0.0) | current | **Hippocratic License 2.1** | Direct dependency — this *is* the React/Leaflet integration layer the whole map UI is built on, not something easily swapped | Not a standard OSI-approved open-source licence — it's an "ethical source" licence that's functionally MIT-like but adds a clause prohibiting use by organisations engaged in specified human-rights violations (war crimes, slavery, human trafficking, etc. — see [the licence text](https://firstdonoharm.dev/version/2/1/license.html)). Extremely unlikely to be a practical problem for this business, but it is a non-standard term a solicitor reviewing the legal pack should see and sign off on explicitly, since "ethical source" licences aren't yet a settled, widely-recognised category the way MIT/Apache are. |
| **`@mapbox/jsonlint-lines-primitives`** | 2.0.2 | **Undeclared** — no `license` field in package.json, no LICENSE file in the package | Deep transitive dependency (JSON validation, likely pulled in via map-style tooling) | Under default copyright law, "no licence" technically means no permission is granted at all. In practice this is very likely an oversight — it's a small Mapbox fork of Zach Carter's classic `jsonlint` (MIT-licensed upstream), same author, package.json just doesn't declare it — but that's an inference, not a confirmed fact. Low practical risk given how deep and small this dependency is, but noting it rather than silently assuming MIT. |

## Checked and confirmed NOT a problem (automated classifier flagged these, manual inspection cleared them)

| Package | Automated label | Actual finding |
|---|---|---|
| `react-leaflet-cluster` 4.1.3 | "Custom: LICENSE" | Read the actual LICENSE file — it's plain, standard MIT text. The classifier just didn't recognise the format. |
| `jsts` 2.7.1 / `@turf/jsts` 2.7.2 | "UNKNOWN" | package.json declares `(EDL-1.0 OR EPL-1.0)` — a dual licence where EDL-1.0 (a permissive BSD-style licence) can be chosen instead of the weaker-copyleft EPL-1.0. No issue. |
| `@maplibre/mlt` 1.1.9 | flagged for review | `(MIT OR Apache-2.0)` — standard permissive dual licence, no issue. |
| `dompurify` 3.3.0 | flagged for review | `(MPL-2.0 OR Apache-2.0)` — Apache-2.0 can be selected, no issue. (Separately has open CVEs — see the security section below, that's a different concern from licensing.) |
| `argparse` 2.0.1 | "Python-2.0" | Python Software Foundation License 2.0 is OSI-approved and permissive (similar terms to BSD/MIT), just an unfamiliar label for a JS project. No issue. |
| `caniuse-lite` (browserslist data) | "CC-BY-4.0" | Standard for this well-known package — it's data, not code, and CC-BY only requires attribution (included in [[11 THIRD_PARTY_NOTICES]]). No issue. |
| `pako` 2.1.0 | "(MIT AND Zlib)" | Both permissive, no issue — Zlib licence text included in notices for completeness. |
| `fibre-tray-react` "UNLICENSED" | — | This is the project's own root `package.json`, not a third-party dependency — the scanner just lists it because it's in the same `node_modules` tree resolution. Not a finding. |

## Security status (separate from licensing, checked as part of the same pass)

**2026-09-05 re-check:** all three items flagged as deliberately unresolved on 2026-08-08 are now resolved. `jspdf` is on 4.2.1 (was 3.0.4), `xlsx` is on 0.20.3 pulled directly from SheetJS's own CDN (`https://cdn.sheetjs.com/xlsx-0.20.3/xlsx-0.20.3.tgz` in `package.json`, was 0.18.5 via npm) — the exact "pull a patched build from SheetJS's own distribution channel" option this register previously flagged as a decision to make — and `uuid` is pinned to 11.1.1 via an explicit `overrides` entry in both `package.json` (root, and nested under `react-d3-tree`) and `functions/package.json`, closing the transitive gap. `npm audit` no longer lists any of the three.

Current `npm audit` state: **2 moderate** in the frontend (`@humanfs/node`, `fflate`, both with a non-breaking fix available) and **1 moderate** in Cloud Functions (`qs`, non-breaking fix available). None force-applied yet — same "not forced through blind" policy as before; these are auto-fixable with `npm audit fix` (no `--force` needed) whenever someone runs it, just not yet actioned as of this note. Down from 16 (frontend) and 15 (functions) on 2026-08-08.

**Historical, for reference — original 2026-08-08 finding:** `npm audit` found 16 vulnerabilities in the frontend (1 low, 4 moderate, 10 high, 1 critical) and 15 in Cloud Functions (1 low, 11 moderate, 3 high). `npm audit fix` (non-breaking only, no `--force`) resolved 12 of 16 frontend vulnerabilities (ajv, brace-expansion, flatted, js-yaml, minimatch, nanoid, picomatch, postcss, rollup, vite, dompurify) and 4 of 15 in Cloud Functions, leaving jspdf/xlsx/uuid tracked above as open until today's re-check.
