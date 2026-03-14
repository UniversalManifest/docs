# WO-0118 — Staging Custom-Domain DNS Cutover Automation

**Status:** COMPLETED  
**Created:** 2026-03-03  
**Updated:** 2026-03-03  
**Priority:** P1  
**Owner:** Platform / CI-CD  
**Source:** Follow-on hardening from WO-0113, WO-0114, and WO-0117
**Completed:** 2026-03-03

## Objective

Automate staging target selection so deploy-gate and synthetic monitoring jobs use custom staging domains when DNS is live, and safely fall back to `pages.dev` / `workers.dev` endpoints when custom domains are not yet reachable.

## Problem Statement

Staging workflows currently require manual base-URL overrides or hardcoded fallback defaults. DNS cutover to `staging.*` domains can create intermittent failures and operational ambiguity until all jobs are switched in lockstep.

## Scope

In scope:

- add reusable staging-target resolution script with reachability checks
- wire both staging verification surfaces to the same resolver logic:
  - deploy gate workflow (`deploy-gated.yml`)
  - synthetic staging workflow (`synthetic-monitoring-staging.yml`)
- document precedence and fallback rules in operations runbooks
- emit clear logs indicating whether `custom`, `fallback`, or `explicit override` targets were used

Out of scope:

- actual Cloudflare DNS record creation
- registrar-level DNS management
- production-domain behavior changes

## Deliverables

1. Target-selection script in `packages/universal-manifest/scripts/`
2. Workflow updates in:
   - `.github/workflows/deploy-gated.yml`
   - `.github/workflows/synthetic-monitoring-staging.yml`
3. Docs updates in:
   - `docs/site/STAGING-PROMOTION-RUNBOOK.md`
   - `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
4. Verification evidence report in `.dev/ai/reports/`

## Acceptance Criteria

- [x] Staging workflows choose custom domains automatically when all required custom staging endpoints are reachable.
- [x] Staging workflows fall back automatically when custom domains are unreachable.
- [x] Operators can still force explicit staging targets through environment/repository variables.
- [x] Workflow logs show selected target set and reason.
- [x] Existing staging smoke and post-deploy verification commands pass under fallback and custom-domain modes (where reachable).

## Dependencies

- `docs/workorders/WO-0113-establish-staging-environments-and-promotion-model.md`
- `docs/workorders/WO-0114-automate-deploy-pipeline-with-release-gates.md`
- `docs/workorders/WO-0117-add-synthetic-monitoring-alerting-and-slo-policy.md`

## Progress Update (2026-03-03)

Repository deliverables completed:

- Added staging target selector:
  - `packages/universal-manifest/scripts/select-staging-bases.mjs`
- Added helper npm script:
  - `packages/universal-manifest/package.json` (`resolve:staging-targets`)
- Updated gated deploy staging verification path to shared selector:
  - `.github/workflows/deploy-gated.yml`
- Updated synthetic staging monitoring path to shared selector:
  - `.github/workflows/synthetic-monitoring-staging.yml`
- Updated staging/synthetic operations docs:
  - `docs/site/STAGING-PROMOTION-RUNBOOK.md`
  - `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`

Verification results:

- `node packages/universal-manifest/scripts/select-staging-bases.mjs --format json` -> selected `fallback_auto` with successful fallback probes
- `eval \"$(node scripts/select-staging-bases.mjs --format shell)\"` + staging smoke/post-deploy commands -> PASS
- post-deploy verification report:
  - `.dev/ai/reports/deploy-checks/2026-03-03T00-14-02-884Z-post-deploy-verification.md`

Operational note:

- GitHub CLI authentication is available locally, but remote workflow evidence for this exact change set requires the branch to exist on GitHub. Run `deploy-gated.yml` and `synthetic-monitoring-staging.yml` after branch publish to capture cloud-run artifacts for this revision.

Cloud run evidence (2026-03-03):

- Synthetic staging monitoring dispatch:
  - `https://github.com/grigb/universal-manifest/actions/runs/22602018555` -> **SUCCESS**
- Deploy gated dispatch (staging-only):
  - `https://github.com/grigb/universal-manifest/actions/runs/22602018536` -> **FAILURE**
  - failure scope: `Verify staging gates` -> `Resolve staging target bases`
  - failure cause: remote `main` checkout missing `packages/universal-manifest/scripts/select-staging-bases.mjs` (`MODULE_NOT_FOUND`)

Remediation implemented in repo:

- Added compatibility fallback in both workflows to resolve staging bases from legacy env defaults when selector script is absent:
  - `.github/workflows/deploy-gated.yml`
  - `.github/workflows/synthetic-monitoring-staging.yml`

Completion addendum (2026-03-03, later pass):

- Custom domains are now active for staging endpoints.
- Provisioning approach uses Worker custom domains (no direct DNS-record API dependency):
  - docs custom domain via staging proxy Worker:
    - `services/staging-docs-proxy/wrangler.toml`
    - `services/staging-docs-proxy/src/index.ts`
  - resolver staging custom domains via:
    - `services/myum-resolver/wrangler.toml` (`[env.staging]` routes with `custom_domain=true`)
- Repository variable cutover completed:
  - `STAGING_DOCS_BASE=https://staging.universalmanifest.net`
  - `STAGING_RESOLVER_BASE=https://staging.myum.net`
  - `STAGING_RESOLVER_WWW_BASE=https://www.staging.myum.net`

Cloud run evidence:

- Synthetic staging monitoring SUCCESS:
  - `https://github.com/grigb/universal-manifest/actions/runs/22602225159`
- Deploy (Gated) staging path SUCCESS:
  - `https://github.com/grigb/universal-manifest/actions/runs/22602253533`
- Provision staging domains workflow SUCCESS:
  - `https://github.com/grigb/universal-manifest/actions/runs/22602353923`
