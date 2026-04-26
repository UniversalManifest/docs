# Synthetic Monitoring, Alerting, and SLO Policy

Status: Active  
Owner: Platform / Operations  
Work Order: WO-0117 (baseline), WO-0215 (error-path coverage extension)  
Last updated: 2026-04-26

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
- `cd packages/universal-manifest && npm run smoke:endpoints:prod:contract` (WO-0215; full status matrix + headers)
- `cd packages/universal-manifest && npm run smoke:endpoints:staging:contract` (WO-0215; full status matrix + headers)
- `cd packages/universal-manifest && npm run verify:postdeploy:prod`
- `cd packages/universal-manifest && node scripts/select-staging-bases.mjs --format json`
- `cd packages/universal-manifest && node scripts/smoke-endpoints.mjs --mode prod --docs-base <selected-docs-base> --resolver-base <selected-resolver-base> [--contract]`
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
- Contract-mode fixture UMIDs (WO-0215; repository variables, not secrets):
  - production: `UM_SMOKE_REDIRECT_UMID`, `UM_SMOKE_REVOKED_UMID`, `UM_SMOKE_CORRUPT_UMID`
  - staging: `UM_SMOKE_REDIRECT_UMID_STAGING`, `UM_SMOKE_REVOKED_UMID_STAGING`, `UM_SMOKE_CORRUPT_UMID_STAGING`
  - When unset the contract suite logs `SKIP <status> (<env-var> not set; ...)` and the status class is excluded from rolling-window calculations rather than poking production into an unsafe state.
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
- `resolver_contract_sli` (added in WO-0215)
  - Definition: successful resolver contract assertions (full status matrix + header
    contract) / total contract assertions in a synthetic run
  - Source: `smoke-endpoints-prod.log` (contract-mode block run via
    `npm run smoke:endpoints:prod:contract`)
  - Status codes covered: `200`, `304`, `400`, `404`, `405`, `OPTIONS preflight`
    (always asserted), plus `307`, `410`, `500` when fixture UMIDs are configured
    (`UM_SMOKE_REDIRECT_UMID`, `UM_SMOKE_REVOKED_UMID`, `UM_SMOKE_CORRUPT_UMID`).
  - Headers asserted: `X-UM-Resolver-Contract`, `X-UM-Resolver-Source`, `ETag`,
    `Cache-Control` (per status), and `Access-Control-Expose-Headers` containing
    the six required tokens defined in `services/myum-resolver/CONTRACT.md` section 3.

## 4) SLO Targets (Rolling 30-Day Window)

Availability targets:

- Docs availability (`docs_availability_sli`): `>= 99.9%`
- Resolver availability (`resolver_availability_sli`): `>= 99.9%`
- Resolver revalidation (`revalidation_sli`): `>= 99.5%`

Error-path / contract availability targets (added in WO-0215):

These targets cover the resolver contract status matrix (CONTRACT.md section 4.5)
and header contract (CONTRACT.md sections 2 and 3). A failure here means an
adopter-visible contract semantic has drifted (e.g., revoked records returning
`404` instead of `410`, or a missing `X-UM-Resolver-Source` header), even if the
happy-path latency probes are passing.

- Resolver contract compliance (`resolver_contract_sli`): `>= 99.9%`
  - Per-status-class success rate measured across always-asserted statuses
    (`200`, `304`, `400`, `404`, `405`, `OPTIONS preflight`).
  - Two consecutive synthetic runs with any contract assertion failing on the
    same status class is a hard alert (see section 6).
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

Latency guardrails (synthetic probe thresholds):

- `https://universalmanifest.net/` <= `1.5s`
- `https://universalmanifest.net/resolver/` <= `2.0s`
- `https://myum.net/health` <= `0.8s`
- `https://myum.net/.well-known/myum-resolver.json` <= `1.0s`
- `https://myum.net/{UMID}` <= `1.2s`

Error budget reference:

- 99.9% objective allows up to 43m 49s unavailability per 30-day window.
- The contract-availability SLO consumes the same error budget as resolver
  availability; a sustained contract violation should be treated as a resolver
  outage even if `/health` is returning 200.

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

### 5.3 Resolver contract status matrix (added in WO-0215)

Run via `npm run smoke:endpoints:prod:contract` (or `:staging:contract` /
`:dev:contract`). Always asserted against the live resolver:

- `200` — direct UMID resolution + full header contract
- `304` — `If-None-Match` revalidation matches prior `ETag`
- `400` — invalid `b64u:` path returns `bad_request`
- `404` — unknown UMID returns `not_found`
- `405` — POST against resolver path returns `method_not_allowed`
- `OPTIONS` — CORS preflight returns 200/204 with required exposed headers

Opt-in (skip with documented reason if the fixture UMID env var is unset, so
production is never poked into an unsafe state):

- `307` — `UM_SMOKE_REDIRECT_UMID` -> deterministic redirect record
- `410` — `UM_SMOKE_REVOKED_UMID` -> deterministic revoked record
- `500` — `UM_SMOKE_CORRUPT_UMID` -> deterministic corrupt KV record (staging only)

Header contract (asserted on every probed response):

- `X-UM-Resolver-Contract: myum-resolver/v0.1`
- `X-UM-Resolver-Source: runtime | kv | fallback_fixture`
- `Cache-Control` matches the contract for that status (`public, max-age=60`
  for 200/304/307; `no-store` for 400/404/405/410/500)
- `Access-Control-Expose-Headers` lists all six required tokens (`etag`,
  `cache-control`, `content-type`, `location`, `x-um-resolver-contract`,
  `x-um-resolver-source`)
- `ETag` present on `200` and matches on `304`
- `Location` present on `307`

## 6) Alert and Escalation Policy

Alert trigger conditions:

1. Sustained availability failure:
   - two consecutive failed scheduled synthetic runs
2. SLO threshold failure:
   - any latency probe above defined threshold in a synthetic run
3. Rolling-window breach:
   - weekly/monthly review indicates SLO objective below target
4. Contract violation detected (added in WO-0215):
   - any failure in the resolver contract status matrix or header contract
     during a synthetic run is a hard alert. Treat the same as a resolver
     outage: see runbook subsection
     `docs/runbooks/PHASE-9-DRIFT-RECOVERY-PLAYBOOK.md` section 2.7.

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
