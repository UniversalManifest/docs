# WO-0121 — Synthetic Alert Delivery and Escalation Drill

**Status:** NOT_STARTED
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

- [ ] `UM_SYNTHETIC_ALERT_WEBHOOK` is configured in repository secrets.
- [ ] Two consecutive synthetic failures trigger alert dispatch.
- [ ] Alert payload includes run URL and status details.
- [ ] Incident record is created and linked in reports.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring-staging.yml`
- `/Users/grig/work/repo/universalmanifest/docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
- `/Users/grig/work/repo/universalmanifest/docs/operations/INCIDENT-REPORT-TEMPLATE.md`
