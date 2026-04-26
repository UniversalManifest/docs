# WO-0117 — Add Synthetic Monitoring, Alerting, and SLO Policy

**Status:** COMPLETED  
**Created:** 2026-03-02  
**Updated:** 2026-03-03  
**Priority:** P1  
**Owner:** Platform / Operations  
**Source:** Follow-on from deployment/runtime hardening review  
**Completed:** 2026-03-02

## Objective

Introduce continuous synthetic monitoring and alerting for adopter-visible endpoints, with explicit SLO definitions and incident-response runbooks.

## Problem Statement

Deploy-time checks exist, but there is no continuously enforced operational contract for uptime, latency, and degradation detection across docs and resolver surfaces.

## Scope

In scope:

- define service-level objectives (availability + latency)
- implement synthetic probes for key endpoints
- route alerts to an accountable channel with escalation policy
- provide operational response runbook

Out of scope:

- full observability platform migration
- custom APM instrumentation beyond synthetic checks

## Deliverables

1. SLO/SLI policy document for:
   - standards/docs domain
   - resolver domain
2. Synthetic check inventory:
   - docs home + critical routes
   - resolver health + well-known + representative UMID resolve + revalidate
3. Alert policy:
   - thresholds
   - paging/escalation path
   - ownership rotation
4. Incident runbook and post-incident evidence template

## Acceptance Criteria

- [x] Synthetic checks run continuously against production and staging surfaces.
- [x] Alerting triggers on sustained endpoint failures and SLO-breach thresholds.
- [x] Owners/escalation paths are documented and tested.
- [x] Incident response runbook is linked from deployment docs.
- [x] Weekly/monthly reliability summary can be generated from monitoring data.

## Dependencies

- `docs/workorders/WO-0113-establish-staging-environments-and-promotion-model.md`
- `docs/workorders/WO-0114-automate-deploy-pipeline-with-release-gates.md`
- `packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `packages/universal-manifest/scripts/post-deploy-verify.mjs`

## Verification Commands (Target)

```bash
cd packages/universal-manifest
npm run smoke:endpoints:prod
npm run verify:postdeploy:prod
```

## Progress Update (2026-03-02)

Repository deliverables completed:

- Added synthetic production monitoring workflow:
  - `.github/workflows/synthetic-monitoring.yml`
- Added synthetic staging monitoring workflow:
  - `.github/workflows/synthetic-monitoring-staging.yml`
- Added SLO/SLI and alert policy:
  - `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
- Added incident/reliability templates:
  - `docs/operations/INCIDENT-REPORT-TEMPLATE.md`
  - `docs/operations/RELIABILITY-SUMMARY-TEMPLATE.md`

Verification results:

- `npm run smoke:endpoints:prod` -> PASS
- `npm run verify:postdeploy:prod` -> PASS
- report generated:
  - `.dev/ai/reports/deploy-checks/2026-03-02T22-25-02-686Z-post-deploy-verification.md`
- staging checks currently fail due unreachable hosts:
  - `npm run smoke:endpoints:staging` -> FAIL (`fetch failed`)
  - `npm run verify:postdeploy:staging` -> FAIL (`fetch failed`)
- fallback-host staging checks:
  - smoke -> PASS
  - post-deploy verify -> PASS
  - report: `.dev/ai/reports/deploy-checks/2026-03-02T22-59-38-831Z-post-deploy-verification.md`

Completion addendum (2026-03-03):

- Staging synthetic monitoring is now passing on custom domains:
  - run: `https://github.com/grigb/universal-manifest/actions/runs/22602225159` -> SUCCESS
- Staging target variables now point to:
  - `https://staging.universalmanifest.net`
  - `https://staging.myum.net`
  - `https://www.staging.myum.net`
- DNS/cutover follow-on is complete through WO-0118 execution and Worker custom-domain provisioning.

Remaining optional enhancement:

1. Configure `UM_SYNTHETIC_ALERT_WEBHOOK` if external alert delivery is desired beyond workflow failure signals.

Reliability summary artifact (latest):

- `.dev/ai/reports/2026-03-03-reliability-summary.md`

## Cross-Reference: WO-0215 (Error-Path Coverage Extension)

WO-0117 established latency-only synthetic monitoring with happy-path coverage.
The 2026-04-26 resolver runtime drift scan found that contract violations on
error-status paths (304, 307, 400, 404, 405, 410, 500) and the header contract
went undetected. WO-0215 extends the SLO policy and synthetic workflows to
assert the full resolver contract status matrix and header contract on every
synthetic run.

- WO-0215: `docs/workorders/WO-0215-extend-synthetic-monitoring-to-full-resolver-contract-coverage.md`
- Contract-mode invocations:
  - `npm run smoke:endpoints:prod:contract`
  - `npm run smoke:endpoints:staging:contract`
- SLO additions: `resolver_contract_sli`, header-contract `100%` per run, opt-in
  `307`/`410`/`500` coverage. See `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
  sections 3, 4, 5.3, and 6.
- Escalation runbook: `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` section 2.7.
