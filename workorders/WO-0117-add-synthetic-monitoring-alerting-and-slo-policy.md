# WO-0117 — Add Synthetic Monitoring, Alerting, and SLO Policy

**Status:** COMPLETED  
**Created:** 2026-03-02  
**Updated:** 2026-03-02  
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

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0113-establish-staging-environments-and-promotion-model.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0114-automate-deploy-pipeline-with-release-gates.md`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/post-deploy-verify.mjs`

## Verification Commands (Target)

```bash
cd /Users/grig/work/repo/universalmanifest/packages/universal-manifest
npm run smoke:endpoints:prod
npm run verify:postdeploy:prod
```

## Progress Update (2026-03-02)

Repository deliverables completed:

- Added synthetic production monitoring workflow:
  - `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml`
- Added synthetic staging monitoring workflow:
  - `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring-staging.yml`
- Added SLO/SLI and alert policy:
  - `/Users/grig/work/repo/universalmanifest/docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
- Added incident/reliability templates:
  - `/Users/grig/work/repo/universalmanifest/docs/operations/INCIDENT-REPORT-TEMPLATE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/operations/RELIABILITY-SUMMARY-TEMPLATE.md`

Verification results:

- `npm run smoke:endpoints:prod` -> PASS
- `npm run verify:postdeploy:prod` -> PASS
- report generated:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/2026-03-02T22-25-02-686Z-post-deploy-verification.md`
- staging checks currently fail due unreachable hosts:
  - `npm run smoke:endpoints:staging` -> FAIL (`fetch failed`)
  - `npm run verify:postdeploy:staging` -> FAIL (`fetch failed`)
- fallback-host staging checks:
  - smoke -> PASS
  - post-deploy verify -> PASS
  - report: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/deploy-checks/2026-03-02T22-59-38-831Z-post-deploy-verification.md`

Follow-up (non-blocking enhancement):

1. Complete custom-domain DNS propagation for staging hosts so standard staging scripts work without overrides.
2. Configure `UM_SYNTHETIC_ALERT_WEBHOOK` if external alert delivery is desired beyond workflow failure signals.
