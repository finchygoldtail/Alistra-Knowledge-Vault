---
status: live
updated: 2026-08-08
related: ["[[Decision Log]]", "[[Security Overview]]", "[[Vercel Deployment]]"]
---

# Secrets Audit — 2026-08-08

Stage 6 of the commercial go-live programme. Scope: current source, full git history (fibre-gis only — AlistraGIS has no `.git`), `.env` handling, Firebase/Vercel config, CI workflows, for both `fibre-gis` (live) and `AlistraGIS` (not live). Tooling: [gitleaks](https://github.com/gitleaks/gitleaks) v8.30.1 against fibre-gis's full commit history (`--log-opts=--all`, 687 commits scanned) and both repos' current working trees.

**No credential values appear anywhere in this document, per programme rule.** Where a value needed inspecting to assess severity, it was read directly from the file and never reproduced.

## Findings

| # | Credential | Service | Where found | Status | Action needed |
|---|---|---|---|---|---|
| 1 | MapTiler API key | MapTiler (map tile provider) | fibre-gis git history (`src/config/mapTiles.ts`, `src/components/JointMapManager.tsx`, multiple commits, oldest 2026-05-01) — already removed from fibre-gis's current source (switched to CARTO's keyless basemap). Same key (matching entropy signature) was **still hardcoded live** in `AlistraGIS/map-frontend/src/config/mapTiles.ts` as a fallback default until fixed today. | **Fixed in AlistraGIS today** — hardcoded fallback removed, now requires `VITE_MAPTILER_KEY` env var, verified absent from the built bundle. Still present in fibre-gis's git history (can't be removed after the fact without a history rewrite, which is its own risk — see note below). | **User action required**: rotate/regenerate this key in the MapTiler account dashboard. Client-side map tile keys are visible to any end user via browser devtools regardless of where they're sourced from in code — the only real protection is (a) rotation if abused, and (b) configuring domain/HTTP-referrer restriction on the key in MapTiler's dashboard, neither of which I can do without account access. |
| 2 | Firebase Web `apiKey` | Firebase (`fibre-gis-v2` project) | Present in both repos' current source (`firebase.ts`) and fibre-gis git history — this is the standard public client config, not a secret. | No action needed | Per [Firebase's own documentation](https://firebase.google.com/docs/projects/api-keys), this key identifies the project but does not grant access — Firebase Auth + Security Rules are the actual access control, and this key is safe to include in client code. Recommend (optional, defense-in-depth) verifying in Google Cloud Console that the key has application restrictions (HTTP referrer) configured, but this is standard hygiene, not a fix for an active exposure. |
| 3 | NVIDIA API key (FRIDAY) | NVIDIA NIM | Google Cloud Secret Manager, via `defineSecret("NVIDIA_API_KEY")` in `functions/src/friday/fridayConfig.ts` | Correct — never in source, never in an env file, injected at runtime only. | None. This is the reference pattern the rest of the app should follow for any future third-party secret. |
| 4 | Functions env file | Firebase Functions config | `functions/.env.fibre-gis-v2` (fibre-gis) | Correctly gitignored (`.env`, `.env.*` in `functions/.gitignore`), confirmed not tracked via `git ls-files`. Contents checked: contains only `FRIDAY_ENABLED` (a feature flag, not a secret). | None. |
| 5 | Vercel Deploy Hook URL | Vercel | Per [[Vercel Deployment]], already deliberately kept out of the vault ("ask Alistair... it's a live credential-equivalent") | Already correctly handled | None — flagging here only to confirm this existing practice is correct and should continue. |
| 6 | Service account files / private keys | Firebase Admin SDK | None found in either repo (`.pem`, `.p12`, `*serviceaccount*` searched) | Correct — Cloud Functions use Application Default Credentials (ADC) via `admin.initializeApp()` with no explicit key file, the correct pattern for code running on Firebase's own infrastructure. | None. |
| 7 | Client-side `VITE_*` env vars | — | `VITE_ALISTRA_BACKEND_STORAGE_API`, `VITE_USE_FUNCTIONS_EMULATOR` (fibre-gis) | Both are feature-flag toggles, not secrets. Vite inlines all `VITE_*` values into the shipped browser bundle, so nothing secret should ever use this prefix. | None found needing a fix — worth remembering as a rule for future additions. |
| 8 | CI workflow (`friday-health.yml`) | GitHub Actions | No secrets referenced at all; `permissions: contents: read` (minimal). | Correct. | None. |

## On the exposed MapTiler key sitting in fibre-gis's git history

Checked whether the GitHub repo behind fibre-gis's `origin` remote (`github.com/finchygoldtail/AlistraGIS` — the local folder is named `fibre-gis` but its remote points at a repo named `AlistraGIS`, confirmed via `git remote -v`) is public: an unauthenticated call to the GitHub API returned `404`, which is consistent with a private repository (GitHub returns 404 rather than 403 for private repos to avoid confirming their existence to outsiders). This **lowers but does not eliminate** the real-world urgency — the key isn't sitting in a location random internet scanners or Google-indexable search would find, but it's still visible to anyone with repo access, and rotation is still the correct move per the programme's "rotate, don't just delete" rule. I could not fully confirm private/public status with certainty from outside the repo; recommend checking directly in GitHub's repo settings.

Removing the key from history entirely would require a git history rewrite (`git filter-repo` or similar) — this is its own risky operation (rewrites commit hashes, breaks any existing clones/forks/PRs, requires a force-push) and is a separate decision from simple rotation. **Rotation alone is sufficient** to neutralize the exposure (the old key stops working; its presence in history becomes harmless), so a history rewrite is not recommended unless there's a separate compliance reason to want it gone entirely.
