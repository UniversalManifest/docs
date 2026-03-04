# WO-0121 — Synthetic Alert Delivery and Escalation Drill

**Status:** COMPLETED
**Created:** 2026-03-04
**Updated:** 2026-03-04
**Priority:** P1
**Owner:** Operations
**Source:** WO-0117 optional enhancement closure

## Objective

Activate and validate external alert delivery for sustained synthetic failures so monitoring is actionable beyond workflow UI visibility.

## Problem Statement

Synthetic monitoring workflows run continuously, but webhook alert dispatch is conditional and skipped when `UM_SYNTHETIC_ALERT_WEBHOOK` is not configured.

## Scope

In scope:

- configure `UM_SYNTHETIC_ALERT_WEBHOOK`
- execute controlled sustained-failure drill to verify alert delivery
- document escalation path and response ownership
- attach incident evidence artifact

Out of scope:

- replacing GitHub Actions monitoring workflows

## Deliverables

1. Configured webhook secret for production/staging monitoring alerts.
2. Drill run artifact proving alert fired on sustained failure condition.
3. Incident response evidence using template.

## Acceptance Criteria

- [x] `UM_SYNTHETIC_ALERT_WEBHOOK` is configured in repository secrets.
- [x] Two consecutive synthetic failures trigger alert dispatch.
- [x] Alert payload includes run URL and status details.
- [x] Incident record is created and linked in reports.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring-staging.yml`
- `/Users/grig/work/repo/universalmanifest/docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/operations/INCIDENT-REPORT-TEMPLATE.md`

## Completion Evidence (2026-03-04)

Repository secret configuration:

- `gh secret list --repo grigb/universal-manifest` shows:
  - `UM_SYNTHETIC_ALERT_WEBHOOK` (updated 2026-03-04T04:55:18Z)

Controlled sustained-failure drill:

- Run 1 (forced failure): `https://github.com/grigb/universal-manifest/actions/runs/22655697651`
- Run 2 (forced failure + webhook dispatch): `https://github.com/grigb/universal-manifest/actions/runs/22655716037`
- Forced UMID: `urn:uuid:99999999-9999-4999-8999-999999999999`

Webhook payload evidence:

- Captured webhook request includes:
  - `run_url`
  - `smoke_exit`
  - `verify_exit`
  - `latency_status`
  - `previous_conclusion`
  - `probe_umid`

Evidence artifacts:

- Drill report:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0121-synthetic-alert-drill-report.md`
- Incident report:
  - `/Users/grig/work/repo/universalmanifest/docs/operations/incidents/INC-2026-03-04-synthetic-alert-drill.md`
- Run-2 log extract:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0121-run2-job.log`
- Webhook capture snapshot:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0121-webhook-requests.json`
