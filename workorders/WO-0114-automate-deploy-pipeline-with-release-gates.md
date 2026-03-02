# WO-0114 — Automate Deploy Pipeline with Release Gates

**Status:** NOT_STARTED  
**Created:** 2026-03-02  
**Priority:** P0  
**Owner:** Platform / CI-CD  
**Source:** Follow-on from deployment/runtime hardening review

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
- [ ] Production deployment can only run after successful staging gate checks.
- [ ] `smoke:endpoints:prod` is enforced against the target environment during release.
- [ ] `verify:postdeploy:prod` report artifacts are generated and archived on each deploy.
- [ ] Production deploy job fails closed if any gate fails.

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
