# WO-0032 — Published docs stale-status scan and fix

**Status:** COMPLETED  
**Created:** 2026-02-22  
**Priority:** HIGH

## Objective

Remove stale "in progress/partially ingested" status language from published docs and verify the published site no longer contains completion-drift statements for finished integration lanes.

## Trigger

User reported stale RP1 published content claiming materialization was still in progress despite completed work.

Problematic published excerpt:
- `site/src/content/docs/integrations/rp1-spatial-fabric.md`
  - "RP1 source materials are partially ingested (Stage -1/0 intake complete)."
  - "fixture/journey materialization is in progress."
  - Internal `.dev/ai` evidence paths shown on public page.

## Scope

In scope:
- scan all published docs under:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/`
- identify stale status statements tied to completed work.
- replace stale statements with current state and public-facing evidence links.
- remove internal `.dev/ai` path leakage from published docs where it appears in stale-status blocks.
- build and deploy updated site.

Out of scope:
- normative spec maturity statements that are intentionally draft (e.g., v0.2 draft notes).

## Acceptance criteria

- [x] Published RP1 page no longer states partial ingestion or in-progress materialization.
- [x] RP1 page status reflects completed fixture/journey materialization.
- [x] RP1 page does not expose internal `.dev/ai` absolute paths.
- [x] Full scan completed for `site/src/content/docs` and findings documented.
- [x] Site build passes (`site` -> `npm run build:clean`).
- [x] Updated site is deployed to Cloudflare Pages and live endpoint check passes.

## Validation commands

- `rg -n -i 'current status|in progress|partially ingested|stage -1/0|materialization is in progress' /Users/grig/work/repo/universalmanifest/site/src/content/docs`
- `rg -n '/Users/grig/work/repo/universalmanifest/\\.dev/ai' /Users/grig/work/repo/universalmanifest/site/src/content/docs`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `node /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/build.mjs`
- `CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 npx --yes wrangler pages deploy /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/dist --project-name universalmanifest-net`

## Completion evidence

- Scan/build/deploy report:
  - `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-22-wo-0032-published-docs-status-scan.md`
- Updated published source page:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`
- Consistency update in repo integration guidance:
  - `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
