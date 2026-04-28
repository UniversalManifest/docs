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

The following secrets are referenced by the monitoring and publication
workflows. Configure them under
`Repository -> Settings -> Secrets and variables -> Actions -> Secrets`.

| Secret name                               | Type / shape                          | Consumed by                                                                                                  | Purpose                                                                                                             | Required? |
|-------------------------------------------|---------------------------------------|--------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|-----------|
| `UM_SYNTHETIC_SMOKE_UMID`                 | UMID string (e.g. `umid:...`)         | `.github/workflows/synthetic-monitoring.yml`, `.github/workflows/synthetic-monitoring-staging.yml`           | Default UMID used by the resolver contract suite when no `workflow_dispatch` `umid` input is supplied.              | Optional  |
| `UM_SYNTHETIC_ALERT_WEBHOOK`              | HTTPS POST webhook URL                | All three monitoring/publication workflows (shared fallback)                                                 | Shared fallback alert webhook (used when an environment-specific webhook secret is not configured).                 | Optional  |
| `UM_SYNTHETIC_ALERT_WEBHOOK_PROD`         | HTTPS POST webhook URL                | `.github/workflows/synthetic-monitoring.yml`, `.github/workflows/publish-spec.yml`                           | Production-only alert webhook. Takes precedence over `UM_SYNTHETIC_ALERT_WEBHOOK` for production failures.          | Optional  |
| `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING`      | HTTPS POST webhook URL                | `.github/workflows/synthetic-monitoring-staging.yml`                                                         | Staging-only alert webhook. Takes precedence over `UM_SYNTHETIC_ALERT_WEBHOOK` for staging failures.                | Optional  |

Note on shapes:

- All three webhook secrets are HTTPS URLs that accept a POST request with
  a JSON body and a `Content-Type: application/json` header. The exact
  upstream service does not matter (Slack incoming webhook, Discord
  webhook, PagerDuty Events v2 endpoint, generic Cloud Run receiver, etc.)
  as long as it accepts the contract documented in
  `Webhook Payload Contract` below.
- `UM_SYNTHETIC_SMOKE_UMID` is treated as a secret because the chosen UMID
  may correspond to a non-public fixture record. Live UMID values are
  never logged.

### Related repository variables (NOT secrets — listed for completeness)

These are configured under
`Repository -> Settings -> Secrets and variables -> Actions -> Variables`
and are referenced by the same monitoring workflows:

- Production fixture UMIDs (added in WO-0215):
  - `UM_SMOKE_REDIRECT_UMID`
  - `UM_SMOKE_REVOKED_UMID`
  - `UM_SMOKE_CORRUPT_UMID`
- Staging fixture UMIDs (added in WO-0215):
  - `UM_SMOKE_REDIRECT_UMID_STAGING`
  - `UM_SMOKE_REVOKED_UMID_STAGING`
  - `UM_SMOKE_CORRUPT_UMID_STAGING`
- Optional staging-target overrides:
  - `STAGING_DOCS_BASE`
  - `STAGING_RESOLVER_BASE`
  - `STAGING_RESOLVER_WWW_BASE`

These are intentionally repository variables (not secrets) because they
are non-sensitive identifiers and are also used as in-workflow log
context. See `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md` section 2
for usage.

## Per-Secret Operator Guide

### `UM_SYNTHETIC_SMOKE_UMID`

- **What it is:** A canonical UMID used by the resolver contract suite as
  the default `200`/`304` probe target. May be a production-published
  manifest or a fixture seeded into the resolver KV namespace.
- **Where to obtain it:** Coordinate with the operator who seeds the
  resolver KV namespace. The UMID must resolve to a manifest that:
  - returns `200` with a stable `ETag` for the `200` assertion;
  - revalidates with `304` against `If-None-Match` for the `304`
    assertion.
- **Workflows that consume it:**
  - `.github/workflows/synthetic-monitoring.yml` (line 81)
  - `.github/workflows/synthetic-monitoring-staging.yml` (line 81)
- **Failure mode if missing:** The workflow falls back to whatever default
  the contract scripts choose. If the scripts have no usable default the
  contract suite logs a `SKIP` line for the affected status class and the
  rolling-window calculation excludes that class. Workflows do not hard
  fail solely from this secret being unset.
- **Override:** A `workflow_dispatch` input (`umid`) is preferred for
  one-off probes; the secret is only consulted when the input is empty.

### `UM_SYNTHETIC_ALERT_WEBHOOK_PROD`

- **What it is:** HTTPS endpoint that accepts `POST application/json` and
  fans out to the on-call channel for production incidents.
- **Where to obtain it:**
  - Slack: create an Incoming Webhook in the on-call workspace, scope it
    to the channel that owns production alerts, copy the webhook URL.
  - PagerDuty: create an Events API v2 routing key and wrap it in a small
    receiver that translates to the contract below, or POST directly to
    the v2 endpoint with a transform proxy.
  - Generic: any HTTPS endpoint that returns `2xx` on POST is acceptable;
    workflows do not parse the response body.
- **Workflows that consume it:**
  - `.github/workflows/synthetic-monitoring.yml` (line 90)
  - `.github/workflows/publish-spec.yml` (line 452)
- **Precedence:** Used first; falls back to `UM_SYNTHETIC_ALERT_WEBHOOK`.
- **Failure mode if missing:** If both this and `UM_SYNTHETIC_ALERT_WEBHOOK`
  are unset, the failure-alert step logs
  `No webhook configured; skipping alert.` and exits `0`. The synthetic
  failure itself still fails the workflow run; only the alert is skipped.

### `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING`

- **What it is:** HTTPS endpoint for staging-only alerts. Often points at
  a less-noisy channel than production (e.g. `#alerts-staging`).
- **Where to obtain it:** Same procedure as the production webhook;
  scope the destination to a staging-only audience.
- **Workflows that consume it:**
  - `.github/workflows/synthetic-monitoring-staging.yml` (line 90)
- **Precedence:** Used first; falls back to `UM_SYNTHETIC_ALERT_WEBHOOK`.
- **Failure mode if missing:** Same as the production webhook fallback —
  alert is skipped, workflow still fails on the underlying assertion.

### `UM_SYNTHETIC_ALERT_WEBHOOK` (shared fallback)

- **What it is:** Single shared HTTPS webhook that catches alerts from
  every environment when an environment-specific webhook is not set.
- **Where to obtain it:** Same procedure as the per-environment webhooks.
- **Workflows that consume it:**
  - `.github/workflows/synthetic-monitoring.yml` (line 91)
  - `.github/workflows/synthetic-monitoring-staging.yml` (line 91)
  - `.github/workflows/publish-spec.yml` (line 453)
- **Precedence:** Last resort; only used when the env-specific webhook is
  empty.
- **Failure mode if missing:** If no environment-specific webhook is set
  AND this is also missing, alerts are skipped (workflows still fail).

## Webhook Payload Contract

All three webhook secrets receive the same shape. The payload is built
inline in each workflow with `jq`:

```json
{
  "text": "Production synthetic monitor failure detected (latency or resolver contract violation)",
  "workflow": "Synthetic Production Monitoring",
  "repository": "<owner>/<repo>",
  "run_url": "https://github.com/<owner>/<repo>/actions/runs/<run-id>",
  "runbook": "docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md#27-alert-contract-violation-detected"
}
```

Variations:

- Staging swaps `"text"` to `"Staging synthetic monitor failure detected ..."`.
- The publish-spec workflow swaps `"text"` to
  `"Spec publication verification failed -- post-publication assertion drift detected"`
  and adds two extra fields (`spec_version`, `ref`).

The receiver MAY ignore unknown fields. The receiver MUST NOT log the
webhook URL itself; the workflows already redact `${WEBHOOK_URL_*}` from
output. Only HTTP status is logged.

## Curl Examples (Webhook Shape — no live secret values)

Use these to verify a webhook before configuring it as a GitHub secret.
**Replace placeholders below with values from your local shell or env;
never paste secret URLs into shared logs.**

### Production-shape probe

```bash
# Set this in your local shell (NOT in shared logs):
#   export WEBHOOK_URL='<paste once, locally only>'

curl -sS -o /dev/null -w '%{http_code}\n' -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "TEST: Production synthetic monitor probe",
    "workflow": "Synthetic Production Monitoring",
    "repository": "OWNER/REPO",
    "run_url": "https://github.com/OWNER/REPO/actions/runs/000000",
    "runbook": "docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md#27-alert-contract-violation-detected"
  }' \
  "$WEBHOOK_URL"
```

### Staging-shape probe

```bash
# export WEBHOOK_URL='<paste once, locally only>'

curl -sS -o /dev/null -w '%{http_code}\n' -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "TEST: Staging synthetic monitor probe",
    "workflow": "Synthetic Staging Monitoring",
    "repository": "OWNER/REPO",
    "run_url": "https://github.com/OWNER/REPO/actions/runs/000000",
    "runbook": "docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md#27-alert-contract-violation-detected"
  }' \
  "$WEBHOOK_URL"
```

### Spec-publication-shape probe

```bash
# export WEBHOOK_URL='<paste once, locally only>'

curl -sS -o /dev/null -w '%{http_code}\n' -X POST \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "TEST: Spec publication verification probe",
    "workflow": "Publish Spec",
    "repository": "OWNER/REPO",
    "ref": "refs/tags/spec-v0.0.0-test",
    "spec_version": "0.0.0-test",
    "run_url": "https://github.com/OWNER/REPO/actions/runs/000000",
    "runbook": "docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md"
  }' \
  "$WEBHOOK_URL"
```

Expected result: `2xx` HTTP status. A `4xx` indicates the payload shape is
rejected by the upstream (e.g. Slack expects a `text` field — present —
plus optional `attachments`). A `5xx` indicates the receiver is unhealthy.

Operational hygiene:

- Always `unset WEBHOOK_URL` after testing.
- Never echo `$WEBHOOK_URL` into shell history or shared transcripts.
- If a webhook URL leaks, rotate it at the upstream provider and update
  the corresponding GitHub Actions secret immediately.

## Rotation Procedure

1. Generate a new webhook URL at the upstream provider (Slack/PagerDuty/etc.).
2. Update the corresponding GitHub Actions secret
   (`UM_SYNTHETIC_ALERT_WEBHOOK*`) via the repo settings UI.
3. Trigger the relevant workflow with `workflow_dispatch` and a known-bad
   input (or temporarily set a latency threshold so the run fails) to
   confirm the new webhook receives the alert.
4. Revoke the old webhook URL at the upstream provider.
5. Record the rotation date in the operator log.

For `UM_SYNTHETIC_SMOKE_UMID`, rotate by re-seeding a fresh fixture UMID
and updating the secret value; coordinate with the resolver KV operator
to avoid breaking in-flight contract assertions.

## Cross-References

- `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md` — SLO targets, SLI
  definitions, alert escalation policy.
- `docs/site/STAGING-PROMOTION-RUNBOOK.md` — staging-to-production
  promotion gates and Cloudflare deploy secrets.
- `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` — incident response
  playbook referenced from the alert payloads.
- `.github/workflows/synthetic-monitoring.yml` — production monitor.
- `.github/workflows/synthetic-monitoring-staging.yml` — staging monitor.
- `.github/workflows/publish-spec.yml` — spec publication verification
  (also fires the production webhook on failure).
