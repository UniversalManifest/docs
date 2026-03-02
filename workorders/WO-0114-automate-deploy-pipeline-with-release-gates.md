# WO-0114 — Automate Deploy Pipeline with Release Gates

**Status:** BLOCKED  
**Created:** 2026-03-02  
**Updated:** 2026-03-02  
**Priority:** P0  
**Owner:** Platform / CI-CD  
**Source:** Follow-on from deployment/runtime hardening review  
**Blocker:** Staging deployment gates cannot be executed end-to-end until staging hosts resolve and environment secrets/variables are provisioned.

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

- [ ] A staging deploy workflow runs on protected trigger and deploys both docs and resolver staging surfaces.
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

External unblock actions required:

1. Configure `CF_ACCOUNT_ID` and `CF_API_TOKEN` secrets in GitHub.
2. Configure `CF_PAGES_PROJECT_STAGING` and `CF_PAGES_PROJECT_PROD` repository variables.
3. Provision/activate staging hosts and run a `workflow_dispatch` dry run (`promote_to_production=false`).
