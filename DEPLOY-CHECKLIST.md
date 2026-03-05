# Deploy Checklist — `universalmanifest.net` + `myum.net`

This checklist is for a first “real” deployment of the Universal Manifest public surfaces:

- `universalmanifest.net` (standards/spec/docs site; static)
- `myum.net/{UMID}` (resolver contract; Worker + KV)

It’s intentionally linear and action-first.

Staging + promotion policy:

- `docs/site/STAGING-PROMOTION-RUNBOOK.md`

## 0) Prereqs

- Cloudflare account with domain control for:
  - `universalmanifest.net`
  - `myum.net`

## 1) Deploy the standards site (`universalmanifest.net`)

Follow:

- `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`

Outcome:

- `https://universalmanifest.net/` loads
- Spec artifacts resolve:
  - `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld`
  - `https://universalmanifest.net/ns/universal-manifest/v0.1/schema.json`
- Harness is available:
  - `https://universalmanifest.net/harness/`

## 2) Deploy the resolver (`myum.net`)

Follow:

- `services/myum-resolver/CLOUDFLARE-DEPLOY.md`

Outcome:

- `https://myum.net/health` returns 200
- `https://myum.net/.well-known/myum-resolver.json` returns 200
- Resolver contract headers match:
  - `services/myum-resolver/CONTRACT.md`

## 3) Run the combined production smoke (required)

This is the fastest “is the system actually live” check:

- `docs/PRODUCTION-DEPLOY-SMOKE.md`

Run:

- `cd packages/universal-manifest && npm run smoke:endpoints:prod`

If this fails, do not claim “published”.

## 4) Evidence capture (recommended)

Capture these as evidence for publishing readiness / future “done-done” packs:

- Smoke output (terminal log)
- Journeys report JSON:
  - `docs/journeys/_artifacts/`
- A harness screenshot (autorun):
  - `https://universalmanifest.net/harness/?autorun=1`

## 5) Continuous monitoring handoff (required)

Confirm synthetic monitoring and alert policy are in place after deploy:

- Policy: `docs/operations/SYNTHETIC-MONITORING-SLO-POLICY.md`
- Workflow: `.github/workflows/synthetic-monitoring.yml`
- Optional alert webhook secrets (environment-specific preferred):
  - `UM_SYNTHETIC_ALERT_WEBHOOK_PROD` (production)
  - `UM_SYNTHETIC_ALERT_WEBHOOK_STAGING` (staging)
  - `UM_SYNTHETIC_ALERT_WEBHOOK` (shared fallback)
- Incident template:
  - `docs/operations/INCIDENT-REPORT-TEMPLATE.md`
