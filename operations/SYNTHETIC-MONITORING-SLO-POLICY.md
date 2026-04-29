# Synthetic Monitoring, Alerting, and SLO Policy

Status: Reference (active monitoring suspended; cron disabled)
Owner: Platform / Operations  
Work Order: WO-0117 (baseline), ~~WO-0215 (error-path coverage extension)~~ — reverted 2026-04-28
Last updated: 2026-04-26 (banner added 2026-04-28)

> **NOTE — 2026-04-28:** WO-0215's expanded error-path coverage and the synthetic-monitoring cron were reverted in commit `e493b3e`. The SLO targets defined here remain the documented intent, but no automated monitoring is currently asserting them. Sections that reference the WO-0215-extended assertions (contract status codes, header contract checks, expanded SLO indicators) describe a posture that does not currently exist in CI.

## 1) Scope

This policy defines reliability objectives and incident handling for production and staging surfaces:

- `https://universalmanifest.net` (standards/spec/docs)
- `https://myum.net` (resolver contract)
- `https://staging.universalmanifest.net` (staging docs custom domain)
- `https://staging.myum.net` (staging resolver custom domain)
- `https://www.staging.myum.net` (staging resolver host variant)
- `https://universalmanifest-net-staging.pages.dev` (staging docs fallback host)
- `https://myum-resolver-staging.grig-624.workers.dev` (staging resolver fallback host)

## 2) Current Monitoring Execution

After revert commit `e493b3e`, synthetic monitoring exists only as
manual-dispatch GitHub Actions workflows:

- Production workflow: `.github/workflows/synthetic-monitoring.yml`
- Staging workflow: `.github/workflows/synthetic-monitoring-staging.yml`
- Trigger mode: `workflow_dispatch` only
- Current schedule state: the `schedule:` blocks remain commented out, so no
  autonomous cron monitoring is running

Current workflow coverage is intentionally narrow:

- Production ping monitor checks:
  - `https://universalmanifest.net/`
  - `https://universalmanifest.net/resolver/`
  - `https://myum.net/health`
- Staging ping monitor checks:
  - `https://staging.universalmanifest.net/`
  - `https://staging.universalmanifest.net/resolver/`
  - `https://staging.myum.net/health`
- Current latency thresholds in workflow code:
  - docs root: `2.5s`
  - docs resolver: `2.0s`
  - resolver health: `0.8s`

Current workflow limitations:

- No `select-staging-bases.mjs` target selection in synthetic monitoring
- No `smoke:endpoints:*` or `verify:postdeploy:*` execution
- No resolver contract suite or WO-0215 status-matrix assertions
- No uploaded workflow artifacts beyond standard Actions logs
- The `workflow_dispatch` `umid` input remains defined but is currently
  unused after the revert

Current alert configuration:

- production preferred: `UM_SYNTHETIC_ALERT_WEBHOOK_PROD`
- staging preferred: `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING`
- shared fallback: `UM_SYNTHETIC_ALERT_WEBHOOK`

For operator onboarding (where to obtain each secret, current webhook
payload contract, curl probes, and rotation procedure) see
`docs/operations/SYNTHETIC-MONITORING-SETUP.md`.

## 3) Reliability Signals

### 3.1 Current workflow-generated signals (manual only)

The live workflows currently provide only three ping-style signals per
environment:

- docs root reachability + latency
- docs resolver reachability + latency
- resolver `/health` reachability + latency

Evidence source: GitHub Actions logs from the two synthetic-monitoring
workflows listed above.

### 3.2 Expanded manual verification (not active monitoring)

These checks still exist and remain useful, but they are not currently part
of any scheduled or automatically alerting workflow:

- `cd packages/universal-manifest && npm run smoke:endpoints:prod`
- `cd packages/universal-manifest && npm run verify:postdeploy:prod`
- `cd packages/universal-manifest && npm run smoke:endpoints:prod:contract`
- `cd packages/universal-manifest && npm run smoke:endpoints:staging:contract`
- `cd packages/universal-manifest && node scripts/smoke-endpoints.mjs --mode prod --docs-base <docs-base> --resolver-base <resolver-base>`
- `cd packages/universal-manifest && node scripts/post-deploy-verify.mjs --mode prod --docs-base <docs-base> --resolver-base <resolver-base> --resolver-www-base <resolver-www-base>`

## 4) SLO Targets (Rolling 30-Day Window)

These targets remain the documented reliability intent. The current
manual-only ping workflows do not continuously measure every target below,
and the contract-specific targets are presently enforced only through manual
verification.

Availability targets:

- Docs availability (`docs_availability_sli`): `>= 99.9%`
- Resolver availability (`resolver_availability_sli`): `>= 99.9%`
- Resolver revalidation (`revalidation_sli`): `>= 99.5%`

Error-path / contract availability targets (manual-only verification after `e493b3e`):

These targets cover the resolver contract status matrix (CONTRACT.md section 4.5)
and header contract (CONTRACT.md sections 2 and 3). A failure here means an
adopter-visible contract semantic has drifted (e.g., revoked records returning
`404` instead of `410`, or a missing `X-UM-Resolver-Source` header), even if the
happy-path latency probes are passing.

- Resolver contract compliance (`resolver_contract_sli`): `>= 99.9%`
  - Per-status-class success rate measured across always-asserted statuses
    (`200`, `304`, `400`, `404`, `405`, `OPTIONS preflight`).
  - Because the contract suite is no longer wired into live workflows, any
    failed manual contract run should be treated as an immediate escalation
    signal (see section 6).
- Header contract compliance: `100%` per run
  - `X-UM-Resolver-Contract` and `X-UM-Resolver-Source` MUST be present on
    every resolver response. A single missing header is treated as a contract
    violation, not a budgeted error.
  - `Access-Control-Expose-Headers` MUST list all six tokens from CONTRACT.md
    section 3 on every CORS-applicable response.
- Opt-in error-path coverage (`307`, `410`, `500`): `>= 99.5%` per status class
  when the corresponding fixture UMID is configured. If a fixture UMID is unset,
  the run logs a `SKIP` line with rationale and the status class is excluded
  from rolling-window calculations.

Latency guardrails:

- Current workflow thresholds:
  - `https://universalmanifest.net/` <= `2.5s`
  - `https://universalmanifest.net/resolver/` <= `2.0s`
  - `https://myum.net/health` <= `0.8s`
- Additional manual verification targets:
  - `https://myum.net/.well-known/myum-resolver.json` <= `1.0s`
  - `https://myum.net/{UMID}` <= `1.2s`

Error budget reference:

- 99.9% objective allows up to 43m 49s unavailability per 30-day window.
- The contract-availability SLO consumes the same error budget as resolver
  availability; a sustained contract violation should be treated as a resolver
  outage even if `/health` is returning 200.

## 5) Current Check Inventory

### 5.1 Live workflow probes

The current manually dispatched workflows check only:

- docs root
- docs resolver
- resolver `/health`

This is true for both production and staging, using the environment-specific
URLs listed in section 2.

### 5.2 Expanded manual checks

When deeper verification is needed, maintainers can run:

- full endpoint smoke (`npm run smoke:endpoints:prod`)
- post-deploy verification (`npm run verify:postdeploy:prod`)
- resolver contract smoke (`npm run smoke:endpoints:prod:contract`)
- staging contract smoke (`npm run smoke:endpoints:staging:contract`)

These checks are valuable, but they are not currently wired into recurring
monitoring or automatic alerting.

## 6) Alert and Escalation Policy

Alert trigger conditions under the current manual-only posture:

1. Manual ping-monitor workflow failure:
   - any failed `synthetic-monitoring.yml` or
     `synthetic-monitoring-staging.yml` run
2. Manual threshold failure:
   - a manually dispatched ping run exceeds one of the current workflow
     latency thresholds
3. Manual contract verification failure:
   - any failed `smoke:endpoints:*:contract` run should be treated as a hard
     resolver alert even though it is no longer emitted by workflow webhook
4. Reliability review breach:
   - weekly/monthly review indicates performance or availability has drifted
     below the intended targets in section 4

Current alert delivery:

- Optional webhook secret precedence:
  - production workflow: `UM_SYNTHETIC_ALERT_WEBHOOK_PROD` -> fallback `UM_SYNTHETIC_ALERT_WEBHOOK`
  - staging workflow: `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING` -> fallback `UM_SYNTHETIC_ALERT_WEBHOOK`
- The current payload contains only `text`, `workflow`, `repository`, and
  `run_url`.
- Webhook response bodies are not logged; only HTTP status is logged.
- No current workflow uploads alert JSON artifacts or embeds runbook links.
- If no webhook secret is configured, the workflow failure still appears in
  Actions history, but no external alert is sent.

Escalation timeline:

1. Initial response target: acknowledge within 15 minutes of a failed manual
   check being noticed
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

- manual synthetic workflow run history (`synthetic-monitoring.yml`,
  `synthetic-monitoring-staging.yml`)
- any saved logs or notes from manual smoke / post-deploy / contract checks
- post-deploy markdown reports in `.dev/ai/reports/deploy-checks/`

Because schedules are disabled, review quality depends on maintainers
actually dispatching checks and preserving the evidence they want reviewed.

Summary outputs should be captured using:

- `docs/operations/RELIABILITY-SUMMARY-TEMPLATE.md`
