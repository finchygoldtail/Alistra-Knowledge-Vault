---
title: Vercel Deployment
type: infrastructure
status: active
owner: Alistair
created: 2026-08-02
updated: 2026-08-09
tags: [vercel, deployment]
---

# Vercel Deployment

Vercel hosts the React, TypeScript and Vite frontend and is the **only** thing that serves `alistragis.com` / `www.alistragis.uk`. Frontend changes go live by pushing to GitHub `main` — Vercel builds and deploys automatically from there. There is no separate manual frontend deploy step.

## Auto-deploy did not fire (2026-08-07, resolved 2026-08-08)

After merging and pushing [[Commercial Subcontracting]] to `main`, no new Vercel deployment appeared — checked via the Vercel API several minutes after the push, versus the ~3 second push-to-deploy gap every prior deployment in this project's history shows. The commit was confirmed present on GitHub `main` (`git ls-remote` matched local `HEAD`), so it was a Vercel-side (or GitHub App/webhook) issue, not a failed push. The Git integration itself was never actually disconnected (verified in the dashboard — Settings → Git → Connected Git Repository showed `finchygoldtail/AlistraGIS`, connected, healthy) — the webhook delivery was just very late; a production deployment of the correct commit eventually went `READY` on its own roughly 3.5 hours after the push.

**Fix applied:** created a Deploy Hook (Settings → Git → Deploy Hooks, name "manual deploy", branch `main`) — a unique unauthenticated `POST` URL that triggers an immediate production deployment of a given branch without waiting on the GitHub webhook. Used it to force a fresh deploy while triaging, confirmed via `GET /v13/deployments/:id` that the resulting deployment was `READY` and aliased to `alistragis.com` + all production domains. **If a future push silently fails to deploy again, POST to the existing Deploy Hook rather than re-diagnosing the webhook** — the hook URL is stored outside this vault (ask Alistair) since it's a live credential-equivalent (unauthenticated trigger).

## Firebase Hosting is not the frontend

`fibre-gis-v2.web.app` (Firebase Hosting) exists but only 301-redirects every path to `https://alistragis.com` (see `firebase.json`'s `redirects` block, added in commit `9bea053` "Clarify Vercel frontend deployment"). Running `firebase deploy --only hosting` updates that redirect-only site and has **zero effect** on what users actually see — nobody's browser loads it directly.

Confirmed the hard way on 2026-08-06: a frontend bug fix was deployed via `firebase deploy --only hosting` and reported as live; the user reloaded `alistragis.com` and got the identical stale bundle, because that command never touched Vercel at all. The fix only went live once pushed to `main`.

**Rule of thumb**: frontend fix → `git push origin main`, full stop. `firebase deploy` is only ever needed for `--only functions` or `--only firestore:rules`.

## 2026-08-09 production release

Commit `7ac3b4d` (`Add safe mobile production completion workflow`) was pushed to GitHub `main`. Vercel created production deployment `dpl_4cnBVZjicrjPbSH5NaCXWM9FnHWg`, reached `READY`, and aliased the release to `alistragis.com`, `www.alistragis.uk`, `alistragis.co.uk` and the Vercel production aliases. The frontend was not deployed through Firebase Hosting because that site remains redirect-only.

## Checks

- Environment variables align with [[Firebase Infrastructure]].
- Deployment status is linked from [[GitHub Workflow]].
- Smoke tests cover [[Main Map]] and authentication.
