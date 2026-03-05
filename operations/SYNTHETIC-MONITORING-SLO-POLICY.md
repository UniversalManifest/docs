# Synthetic Monitoring, Alerting, and SLO Policy

Status: Active  
Owner: Platform / Operations  
Work Order: WO-0117  
Last updated: 2026-03-04

## 1) Scope

This policy defines reliability objectives and incident handling for production and staging surfaces:

- `https://universalmanifest.net` (standards/spec/docs)
- `https://myum.net` (resolver contract)
- `https://staging.universalmanifest.net` (staging docs custom domain)
- `https://staging.myum.net` (staging resolver custom domain)
- `https://www.staging.myum.net` (staging resolver host variant)
- `https://universalmanifest-net-staging.pages.dev` (staging docs fallback host)
- `https://myum-resolver-staging.grig-624.workers.dev` (staging resolver fallback host)

## 2) Synthetic Monitoring Execution

Monitoring is executed by:

- Production workflow: `.github/workflows/synthetic-monitoring.yml`
- Staging workflow: `.github/workflows/synthetic-monitoring-staging.yml`
- Shared staging target selector: `packages/universal-manifest/scripts/select-staging-bases.mjs`
- Triggers:
  - scheduled every 15 minutes
  - manual via `workflow_dispatch`

Staging target precedence in monitoring workflow:

1. explicit override variables (`STAGING_DOCS_BASE`, `STAGING_RESOLVER_BASE`, optional `STAGING_RESOLVER_WWW_BASE`)
2. custom staging domains (`staging.universalmanifest.net`, `staging.myum.net`, `www.staging.myum.net`) when all probes are reachable
3. fallback hosts (`pages.dev` + `workers.dev`) when custom-domain probes fail

Current operational mode (2026-03-03):

- custom-domain staging probes are passing in cloud execution:
  - `https://github.com/grigb/universal-manifest/actions/runs/22602225159`

The workflows use existing verification scripts:

- `cd packages/universal-manifest && npm run smoke:endpoints:prod`
- `cd packages/universal-manifest && npm run verify:postdeploy:prod`
- `cd packages/universal-manifest && node scripts/select-staging-bases.mjs --format json`
- `cd packages/universal-manifest && node scripts/smoke-endpoints.mjs --mode prod --docs-base <selected-docs-base> --resolver-base <selected-resolver-base>`
- `cd packages/universal-manifest && node scripts/post-deploy-verify.mjs --mode prod --docs-base <selected-docs-base> --resolver-base <selected-resolver-base> --resolver-www-base <selected-resolver-www-base>`

Generated monitoring artifacts:

- `packages/universal-manifest/artifacts/smoke-endpoints-prod.log`
- `packages/universal-manifest/artifacts/smoke-endpoints-staging.log`
- `packages/universal-manifest/artifacts/post-deploy-verify.log`
- `packages/universal-manifest/artifacts/post-deploy-verify-staging.log`
- `packages/universal-manifest/artifacts/latency-probes.txt`
- `.dev/ai/reports/deploy-checks/*-post-deploy-verification.md`

Optional check configuration:

- `UM_SYNTHETIC_SMOKE_UMID` (secret) for production UMID override
- `workflow_dispatch` input `umid` (manual one-off override)
- `STAGING_DOCS_BASE` / `STAGING_RESOLVER_BASE` / `STAGING_RESOLVER_WWW_BASE` repository variables for explicit staging target override
- Alert webhook secrets (environment-specific preferred):
  - production: `UM_SYNTHETIC_ALERT_WEBHOOK_PROD`
  - staging: `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING`
  - shared fallback: `UM_SYNTHETIC_ALERT_WEBHOOK`

## 3) SLI Definitions

SLIs are calculated from synthetic runs and retained artifacts:

- `docs_availability_sli`
  - Definition: successful docs endpoint checks / total docs endpoint checks
  - Source: `smoke-endpoints-prod.log`
- `resolver_availability_sli`
  - Definition: successful resolver endpoint checks / total resolver endpoint checks
  - Source: `smoke-endpoints-prod.log` + post-deploy checks
- `revalidation_sli`
  - Definition: successful resolver `ETag` revalidate (`304`) checks / total revalidate checks
  - Source: `smoke-endpoints-prod.log`
- `synthetic_latency_sli`
  - Definition: endpoint response time sampled each synthetic run
  - Source: `latency-probes.txt`

## 4) SLO Targets (Rolling 30-Day Window)

Availability targets:

- Docs availability (`docs_availability_sli`): `>= 99.9%`
- Resolver availability (`resolver_availability_sli`): `>= 99.9%`
- Resolver revalidation (`revalidation_sli`): `>= 99.5%`

Latency guardrails (synthetic probe thresholds):

- `https://universalmanifest.net/` <= `1.5s`
- `https://universalmanifest.net/resolver/` <= `2.0s`
- `https://myum.net/health` <= `0.8s`
- `https://myum.net/.well-known/myum-resolver.json` <= `1.0s`
- `https://myum.net/{UMID}` <= `1.2s`

Error budget reference:

- 99.9% objective allows up to 43m 49s unavailability per 30-day window.

## 5) Synthetic Check Inventory

### 5.1 Docs checks

From `smoke-endpoints.mjs` in production mode:

- `/`
- `/conformance/resolver/`
- `/harness/index.html`
- `/sandbox/`
- `/resolver/`
- `/ns/universal-manifest/v0.1/schema.jsonld`
- `/404.html`

### 5.2 Resolver checks

From `smoke-endpoints.mjs` and `post-deploy-verify.mjs`:

- `/health`
- `/.well-known/myum-resolver.json`
- `/{UMID}` (direct)
- `/b64u:{UMID}` (base64url format)
- `ETag` + `If-None-Match` revalidate path (`304`)
- `x-um-resolver-contract` and exposed header checks

## 6) Alert and Escalation Policy

Alert trigger conditions:

1. Sustained availability failure:
   - two consecutive failed scheduled synthetic runs
2. SLO threshold failure:
   - any latency probe above defined threshold in a synthetic run
3. Rolling-window breach:
   - weekly/monthly review indicates SLO objective below target

Alert delivery:

- Optional webhook secret precedence:
  - production workflow: `UM_SYNTHETIC_ALERT_WEBHOOK_PROD` -> fallback `UM_SYNTHETIC_ALERT_WEBHOOK`
  - staging workflow: `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING` -> fallback `UM_SYNTHETIC_ALERT_WEBHOOK`
- If a webhook secret is configured and sustained failure is detected, workflow posts an alert payload with run metadata and status details.
- Webhook response bodies are not logged; only HTTP status is logged to reduce secret/token leakage risk.
- Alert payload JSON is persisted in workflow artifacts (`packages/universal-manifest/artifacts/webhook-alert-*.json`) for auditability.
- If secret is not configured, workflow still fails and stores artifacts for manual triage.

Escalation timeline:

1. Initial response target: acknowledge within 15 minutes
2. If unresolved after 30 minutes: escalate to platform maintainer
3. If unresolved after 60 minutes: declare SEV incident and start incident log

## 7) Incident Runbooks and Templates

Runbooks:

- `docs/PRODUCTION-DEPLOY-SMOKE.md`
- `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
- `services/myum-resolver/CLOUDFLARE-DEPLOY.md`

Templates:

- Incident report: `docs/operations/INCIDENT-REPORT-TEMPLATE.md`
- Reliability summary: `docs/operations/RELIABILITY-SUMMARY-TEMPLATE.md`

## 8) Weekly/Monthly Reliability Review

Review cadence:

- Weekly: availability and latency trend review
- Monthly: SLO compliance and error-budget consumption review

Minimum review inputs:

- synthetic workflow run history (`synthetic-monitoring.yml`, `synthetic-monitoring-staging.yml`)
- artifact logs (`smoke-endpoints-prod.log`, `smoke-endpoints-staging.log`, `post-deploy-verify.log`, `post-deploy-verify-staging.log`, `latency-probes.txt`)
- post-deploy markdown reports in `.dev/ai/reports/deploy-checks/`

Summary outputs should be captured using:

- `docs/operations/RELIABILITY-SUMMARY-TEMPLATE.md`
