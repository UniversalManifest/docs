# WO-0019 — Resolver J03 reliability and routing hardening

**Status:** COMPLETED  
**Created:** 2026-02-20

## Objective

Clear immediate production/interoperability blockers by:

1. fixing local resolver E2E instability in journey `J03`,
2. deploying the latest docs/tooling build so workbench routes are live,
3. routing `www.myum.net` to the resolver worker contract.

## Scope

In scope:

- make `npm run journeys` pass `5/5` deterministically for local execution.
- ensure Cloudflare Pages serves the latest workbench routes.
- ensure resolver triggers include both `myum.net/*` and `www.myum.net/*`.
- re-run production endpoint smoke and capture evidence.

Out of scope:

- external reader-testing execution for `WO-0015`.
- RP1 corpus ingestion and synthesis implementation.

## Deliverables

- `packages/universal-manifest/scripts/run-journeys.mjs`
- `services/myum-resolver/wrangler.toml`
- `docs/journeys/_artifacts/2026-02-20T05-25-51-070Z-journey-report.json`
- Historical K2B completeness report referenced by this WO is not present in the current checkout.

## Acceptance criteria

- [x] `npm run journeys` passes `5/5` with no failures.
- [x] `https://universalmanifest.net/getting-started/workbench/` resolves `200`.
- [x] `https://universalmanifest.net/getting-started/workbench/` resolves to live content (`308` redirect to `/workbench/`, then `200`).
- [x] `https://www.myum.net/health` resolves `200`.
- [x] `npm run smoke:endpoints:prod` passes after deployment/routing updates.

## Completion evidence

- Journeys pass:
  - command: `cd packages/universal-manifest && npm run journeys`
  - artifact: `docs/journeys/_artifacts/2026-02-20T05-25-51-070Z-journey-report.json`
- Pages deployment:
  - command: `CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 npx --yes wrangler pages deploy deploy/universalmanifest.net/dist --project-name universalmanifest-net`
  - deployment URL: `https://5f6a06d8.universalmanifest-net.pages.dev`
- Resolver routing deployment:
  - command: `cd services/myum-resolver && CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 ./node_modules/.bin/wrangler deploy`
  - deployed triggers include:
    - `myum.net/*`
    - `www.myum.net/*`
- Production checks:
  - `https://universalmanifest.net/getting-started/workbench/` -> `200`
  - `https://universalmanifest.net/getting-started/workbench/` -> `308` (`Location: /workbench/`)
  - `https://universalmanifest.net/workbench/` -> `200`
  - `https://www.myum.net/health` -> `200`
  - `cd packages/universal-manifest && npm run smoke:endpoints:prod` -> `PASS`

## Dependencies

- `docs/workorders/WO-0012-user-journeys-and-e2e-test-suite.md`
- `docs/workorders/WO-0003-publishing-and-release.md`
- `docs/reports/2026-02-20-master-forward-worklist.md`
