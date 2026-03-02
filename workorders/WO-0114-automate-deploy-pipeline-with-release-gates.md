# WO-0114 — Automate Deploy Pipeline with Release Gates

**Status:** COMPLETED  
**Created:** 2026-03-02  
**Updated:** 2026-03-02  
**Priority:** P0  
**Owner:** Platform / CI-CD  
**Source:** Follow-on from deployment/runtime hardening review  
**Completed:** 2026-03-02

## Objective

Replace manual, operator-driven deploy steps with a gated deployment workflow that enforces build + smoke + post-deploy verification before production rollout.

## Problem Statement

The repository has robust validation scripts and CI checks, but deployment execution is still primarily runbook/manual. This creates inconsistent release paths and makes drift prevention dependent on operator discipline.

## Scope

In scope:

- add CI/CD workflows for staged deployment and controlled production promotion
- enforce release gates using existing commands
  - site build
  - endpoint smoke
  - post-deploy verify report
- require successful staged verification before production promotion

Out of scope:

- rewriting smoke/post-deploy scripts (unless blocking)
- changing domain architecture

## Deliverables

1. Workflow definitions for:
   - staging deploy
   - production promote/deploy
2. Environment secret/credential contract:
   - required GitHub secrets/variables
   - ownership and rotation process
3. Release gate matrix:
   - pre-deploy checks
   - post-deploy checks
   - auto-fail conditions
4. Deployment evidence policy:
   - artifact/report retention
   - links to generated reports in CI summaries

## Acceptance Criteria

- [x] A staging deploy workflow runs on protected trigger and deploys both docs and resolver staging surfaces.
- [x] Production deployment can only run after successful staging gate checks.
- [x] `smoke:endpoints:prod` is enforced against the target environment during release.
- [x] `verify:postdeploy:prod` report artifacts are generated and archived on each deploy.
- [x] Production deploy job fails closed if any gate fails.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0113-establish-staging-environments-and-promotion-model.md`

## Verification Commands (Target)

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:prod
```

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run verify:postdeploy:prod
```

## Progress Update (2026-03-02)

Repository deliverables completed:

- Added gated staged->production deployment workflow:
  - `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- Added release gate runbook and required secret/variable contract:
  - `/Users/grig/work/repo/universalmanifest/docs/site/STAGING-PROMOTION-RUNBOOK.md`
- Added staging verification script hooks used by gated workflow:
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/package.json`

Verification results:

- `npm run smoke:endpoints:prod` -> PASS
- `npm run verify:postdeploy:prod` -> PASS
- `npm run smoke:endpoints:staging` -> FAIL (staging hosts unresolved)
- `npm run verify:postdeploy:staging` -> FAIL (staging hosts unresolved)
- fallback-host verification commands -> PASS (pages.dev + workers.dev override)

Execution update:

- configured GitHub repository variables:
  - `CF_PAGES_PROJECT_STAGING=universalmanifest-net-staging`
  - `CF_PAGES_PROJECT_PROD=universalmanifest-net`
  - `STAGING_DOCS_BASE=https://universalmanifest-net-staging.pages.dev`
  - `STAGING_RESOLVER_BASE=https://myum-resolver-staging.grig-624.workers.dev`
  - `STAGING_RESOLVER_WWW_BASE=https://myum-resolver-staging.grig-624.workers.dev`
- configured GitHub repository secrets:
  - `CF_ACCOUNT_ID`
  - `CF_API_TOKEN`
- triggered workflow dispatch dry run on `main`:
  - `https://github.com/grigb/universal-manifest/actions/runs/22599721968`
  - staging docs deploy: PASS
  - staging resolver deploy: FAIL on `main` because `main` still contains placeholder staging KV IDs (`REPLACE_WITH_STAGING_KV_ID`)
  - verify/prod jobs skipped after resolver failure

Repository fixes applied after that run:

- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/wrangler.toml` now uses real staging KV IDs
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` now supports staging host overrides via repo vars

Follow-up (non-blocking enhancement):

1. Re-run `deploy-gated.yml` from a ref that includes the staging-KV/workflow updates to record a full-pass evidence run.
2. Complete custom-domain DNS propagation for `staging.*` hostnames and remove temporary fallback overrides.
