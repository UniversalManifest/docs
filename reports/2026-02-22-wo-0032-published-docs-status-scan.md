# WO-0032 Report — Published Docs Stale-Status Scan and Fix

Date: 2026-02-22
Work order: docs/workorders/WO-0032-published-docs-stale-status-scan-and-fix.md

## Scope scanned

- site/src/content/docs/

## Findings

1. Stale published RP1 status block (fixed)
- File: site/src/content/docs/integrations/rp1-spatial-fabric.md
- Old content incorrectly stated partial ingestion and in-progress materialization.
- Old content exposed internal `.dev/ai` absolute paths on a public page.

2. Additional stale-status issues in published docs
- None found after full scan with stale-status phrase and internal-path checks.

## Changes applied

- Updated public RP1 integration page status to completed-state language.
- Replaced internal `.dev/ai` evidence links with public evidence links:
  - /harness/fixtures/v0.1/stubs/rp1-spatial-fabric-manifest.jsonld
  - /proof/journeys/
- Updated repo integration source page for consistency:
  - integrations/rp1-spatial-fabric.md

## Scan commands and results

- `rg -n -i 'partially ingested|stage -1/0|materialization is in progress|fixture/journey materialization pending|source corpus is now partially imported' site/src/content/docs`
  - Result: no matches after fix.

- `rg -n '\\.dev/ai' site/src/content/docs`
  - Result: no matches after fix.

## Build and deploy

- Site build:
  - `cd site && npm run build:clean`
  - Result: PASS.

- Publish bundle build:
  - `node deploy/universalmanifest.net/build.mjs`
  - Result: PASS.

- Cloudflare Pages deploy (production):
  - `CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 npx --yes wrangler pages deploy deploy/universalmanifest.net/dist --project-name universalmanifest-net --branch main`
  - Deployment ID: `ed663d39-d97a-4bfe-8f83-bff4e84a46e1`
  - Environment: Production

## Live verification

- Route: https://universalmanifest.net/integrations/rp1-spatial-fabric/
- Verified present text:
  - `RP1 lane materialization is complete for the current scope.`
  - `Public implementation evidence:`
- Verified absent text:
  - `partially ingested`
  - `Stage -1/0`
  - `materialization is in progress`

