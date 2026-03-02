# WO-0117 — Add Synthetic Monitoring, Alerting, and SLO Policy

**Status:** NOT_STARTED  
**Created:** 2026-03-02  
**Priority:** P1  
**Owner:** Platform / Operations  
**Source:** Follow-on from deployment/runtime hardening review

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

- [ ] Synthetic checks run continuously against production and staging surfaces.
- [ ] Alerting triggers on sustained endpoint failures and SLO-breach thresholds.
- [ ] Owners/escalation paths are documented and tested.
- [ ] Incident response runbook is linked from deployment docs.
- [ ] Weekly/monthly reliability summary can be generated from monitoring data.

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
