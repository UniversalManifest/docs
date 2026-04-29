# Synthetic Monitoring Setup (Secrets and Webhook Configuration)

Status: Reference (synthetic-monitoring crons currently disabled)
Owner: Platform / Operations
Work Order: WO-0236 (operator onboarding hygiene)
Last updated: 2026-04-26 (banner added 2026-04-28)

> **NOTE — 2026-04-28:** The synthetic-monitoring workflows were reverted to their budget-zero state in commit `e493b3e` (cron schedules commented out per the prior `93683fe` cost-control commit). The secrets documented below still apply IF a maintainer re-enables the schedules; until then, this document is reference material only and no automated probes are running.

## Purpose

This runbook is the operator-onboarding companion to
`docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`. It enumerates every
GitHub Actions secret that the synthetic monitoring workflows consume,
explains where to obtain each value, and documents what fails if a value is
missing. New maintainers should be able to wire up alerting end-to-end
using only this document.

## Location Choice and Rationale

This file is created at `docs/operations/SYNTHETIC-MONITORING-SETUP.md`
rather than being appended to `docs/site/STAGING-PROMOTION-RUNBOOK.md`
because:

- The staging promotion runbook is already large and is scoped to the
  release flow (deploy gates, smoke gates, rollback). Synthetic monitoring
  setup is a distinct operational concern (alerting, observability,
  on-call wiring) and lives more naturally next to the SLO policy.
- The SLO policy doc (`docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`)
  already references these secret names by purpose; this file gives
  operators the matching "where to obtain / how to set / what breaks if
  unset" guide and is cross-linked from the SLO policy doc.
- Future monitoring secret additions (e.g. additional fixture UMIDs or
  a webhook for a new alerting backend) can be appended here without
  bloating the staging runbook further.

## Secret Inventory (Names and Shapes Only — never paste live values)

After revert commit `e493b3e`, the currently live synthetic-monitoring
workflows consume only alert-webhook secrets. Configure them under
`Repository -> Settings -> Secrets and variables -> Actions -> Secrets`.

| Secret name                          | Type / shape           | Consumed by                                             | Purpose                                                                                           | Required? |
|--------------------------------------|------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------|
| `UM_SYNTHETIC_ALERT_WEBHOOK`         | HTTPS POST webhook URL | `.github/workflows/synthetic-monitoring.yml`, `.github/workflows/synthetic-monitoring-staging.yml` | Shared fallback alert webhook when an environment-specific secret is not configured.              | Optional  |
| `UM_SYNTHETIC_ALERT_WEBHOOK_PROD`    | HTTPS POST webhook URL | `.github/workflows/synthetic-monitoring.yml`            | Production-only alert webhook. Takes precedence over `UM_SYNTHETIC_ALERT_WEBHOOK` for prod runs. | Optional  |
| `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING` | HTTPS POST webhook URL | `.github/workflows/synthetic-monitoring-staging.yml`    | Staging-only alert webhook. Takes precedence over `UM_SYNTHETIC_ALERT_WEBHOOK` for staging runs. | Optional  |

Note on shapes:

- All webhook secrets are HTTPS URLs that accept a POST request with a JSON
  body and a `Content-Type: application/json` header.
- The current workflows do not parse response bodies; they only require the
  receiver to accept the request successfully.

### Historical monitoring inputs (not currently consumed)

The following inputs were used by the reverted WO-0215 contract-monitoring
expansion and are not consumed by the current workflows:

- `UM_SYNTHETIC_SMOKE_UMID`
- `UM_SMOKE_REDIRECT_UMID`
- `UM_SMOKE_REVOKED_UMID`
- `UM_SMOKE_CORRUPT_UMID`
- `UM_SMOKE_REDIRECT_UMID_STAGING`
- `UM_SMOKE_REVOKED_UMID_STAGING`
- `UM_SMOKE_CORRUPT_UMID_STAGING`

The `workflow_dispatch` `umid` input still exists in the workflow files, but
after `e493b3e` it is currently unused because the contract-suite steps were
removed. Treat these names as historical unless contract monitoring is
explicitly reintroduced later.

## Per-Secret Operator Guide

### `UM_SYNTHETIC_ALERT_WEBHOOK_PROD`

- **What it is:** HTTPS endpoint that accepts `POST application/json` and
  fans out to the on-call channel for production ping-monitor failures.
- **Where to obtain it:**
  - Slack: create an Incoming Webhook in the on-call workspace, scope it to
    the production-alerts channel, and copy the webhook URL.
  - PagerDuty: create or reuse a receiver that accepts the JSON contract
    below and forwards it into the desired escalation path.
  - Generic: any HTTPS endpoint that returns `2xx` on POST is acceptable.
- **Workflow that consumes it:** `.github/workflows/synthetic-monitoring.yml`
- **Precedence:** Used first; falls back to `UM_SYNTHETIC_ALERT_WEBHOOK`.
- **Failure mode if missing:** If both this and `UM_SYNTHETIC_ALERT_WEBHOOK`
  are unset, the workflow logs `No webhook configured; skipping alert.` and
  exits the alert step successfully. The ping failure still fails the
  workflow run.

### `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING`

- **What it is:** HTTPS endpoint for staging-only ping-monitor alerts.
- **Where to obtain it:** Same procedure as the production webhook; scope the
  receiver to a staging-only audience if you want lower noise.
- **Workflow that consumes it:** `.github/workflows/synthetic-monitoring-staging.yml`
- **Precedence:** Used first; falls back to `UM_SYNTHETIC_ALERT_WEBHOOK`.
- **Failure mode if missing:** Same as the production case; the alert is
  skipped, but the failed workflow run remains failed.

### `UM_SYNTHETIC_ALERT_WEBHOOK` (shared fallback)

- **What it is:** Single shared HTTPS webhook that catches production or
  staging ping-monitor failures when an environment-specific webhook is not
  set.
- **Where to obtain it:** Same procedure as the per-environment webhooks.
- **Workflows that consume it:**
  - `.github/workflows/synthetic-monitoring.yml`
  - `.github/workflows/synthetic-monitoring-staging.yml`
- **Precedence:** Last resort; only used when the env-specific webhook is
  empty.
- **Failure mode if missing:** Alerts are skipped, but workflow failures are
  still visible in Actions history.

## Webhook Payload Contract

The current workflows send a small JSON payload built inline with `jq`:

```json
{
  "text": "Production Ping Monitor failure detected",
  "workflow": "Synthetic Production Monitoring",
  "repository": "<owner>/<repo>",
  "run_url": "https://github.com/<owner>/<repo>/actions/runs/<run-id>"
}
```

Variations:

- Staging swaps `"text"` to `"Staging Ping Monitor failure detected"`.
- No current workflow includes `runbook`, `spec_version`, or `ref` fields.

The receiver MAY ignore unknown fields. The receiver MUST NOT log the webhook
URL itself.

## Curl Examples (Webhook Shape — no live secret values)

Use these to verify a webhook before configuring it as a GitHub secret.
**Replace placeholders below with values from your local shell or env; never
paste secret URLs into shared logs.**

### Production-shape probe

```bash
# Set this in your local shell (NOT in shared logs):
#   export WEBHOOK_URL='<paste once, locally only>'

curl -sS -o /dev/null -w '%{http_code}\n' -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "TEST: Production ping monitor probe",
    "workflow": "Synthetic Production Monitoring",
    "repository": "OWNER/REPO",
    "run_url": "https://github.com/OWNER/REPO/actions/runs/000000"
  }' \
  "$WEBHOOK_URL"
```

### Staging-shape probe

```bash
# export WEBHOOK_URL='<paste once, locally only>'

curl -sS -o /dev/null -w '%{http_code}\n' -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "TEST: Staging ping monitor probe",
    "workflow": "Synthetic Staging Monitoring",
    "repository": "OWNER/REPO",
    "run_url": "https://github.com/OWNER/REPO/actions/runs/000000"
  }' \
  "$WEBHOOK_URL"
```

Expected result: `2xx` HTTP status. A `4xx` indicates the payload shape is
rejected by the upstream. A `5xx` indicates the receiver is unhealthy.

Operational hygiene:

- Always `unset WEBHOOK_URL` after testing.
- Never echo `$WEBHOOK_URL` into shell history or shared transcripts.
- If a webhook URL leaks, rotate it at the upstream provider and update the
  corresponding GitHub Actions secret immediately.

## Rotation Procedure

1. Generate a new webhook URL at the upstream provider (Slack/PagerDuty/etc.).
2. Update the corresponding GitHub Actions secret
   (`UM_SYNTHETIC_ALERT_WEBHOOK*`) via the repo settings UI.
3. Validate the new receiver with the local curl probe above before relying
   on it in Actions.
4. Revoke the old webhook URL at the upstream provider.
5. Record the rotation date in the operator log.

## Cross-References

- `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md` — current monitoring
  posture, SLO targets, and escalation policy.
- `docs/site/STAGING-PROMOTION-RUNBOOK.md` — staging-to-production deploy
  verification and Cloudflare deploy secrets.
- `.github/workflows/synthetic-monitoring.yml` — production ping monitor.
- `.github/workflows/synthetic-monitoring-staging.yml` — staging ping monitor.
