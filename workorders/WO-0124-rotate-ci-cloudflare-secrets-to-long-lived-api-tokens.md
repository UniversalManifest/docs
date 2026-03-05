# WO-0124 — Rotate CI Cloudflare Secrets to Long-Lived API Tokens

**Status:** COMPLETED
**Created:** 2026-03-04
**Updated:** 2026-03-05
**Priority:** P0
**Owner:** Platform / DevOps
**Source:** Post-WO-0123 durability hardening

## Objective

Replace time-bound Wrangler OAuth-derived CI secrets with long-lived Cloudflare API tokens scoped for staging and production deploy workflows.

## Problem Statement

WO-0123 restored green production promotions using environment-scoped secrets, but durability needed to be proven with API-token enforcement and fresh production validation evidence.

## Scope

In scope:
- create long-lived Cloudflare API tokens for staging and production deployment paths
- rotate GitHub environment secrets to these tokens
- validate with at least one gated production promotion and one synthetic production monitoring run

Out of scope:
- resolver contract changes
- frontend changes

## Deliverables

1. New long-lived Cloudflare deploy tokens issued and documented in secure ops runbook.
2. GitHub env secrets updated:
- `CF_API_TOKEN_STAGING`
- `CF_API_TOKEN_PRODUCTION`
3. Validation evidence of green deploy + synthetic runs after rotation.

## Acceptance Criteria

- [x] Gated production promotion run succeeds after token rotation.
- [x] Production synthetic monitoring run succeeds after token rotation.
- [x] No dependence on time-bound OAuth access token material for CI deploys.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0123-cloudflare-credential-stabilization-for-gated-production-promotions.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0123-credential-stabilization-closeout.md`

## Execution Progress (2026-03-04)

Completed in this pass:
- Added Cloudflare auth preflight checks to all deploy jobs in gated workflow:
  - `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- Validated preflight-enabled workflow on production promotion path:
  - Run: https://github.com/grigb/universal-manifest/actions/runs/22659009192 (`success`)
  - All staging + production jobs passed.
- Added Cloudflare auth type telemetry and optional API-token enforcement switch (`CF_REQUIRE_API_TOKEN*`) in deploy preflight.
- Validated auth-type telemetry-enabled production promotion:
  - Run: https://github.com/grigb/universal-manifest/actions/runs/22659202729 (`success`)
  - All staging + production jobs passed.
- Corrected API-token enforcement match logic to accept Cloudflare `Account API Token` auth type string variants in all deploy jobs.
  - Commit: `e15fd8ef1fa816b97ff64417300f265e305ff4c4`
  - File: `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- Enabled token-only enforcement flags in GitHub environments:
  - staging var: `CF_REQUIRE_API_TOKEN_STAGING=true`
  - production var: `CF_REQUIRE_API_TOKEN_PRODUCTION=true`
- Validated enforced API-token gating with full production promotion:
  - Run: https://github.com/grigb/universal-manifest/actions/runs/22659412126 (`success`)
  - All staging + production deploy and verify jobs passed.
  - Preflight auth type in deploy jobs: `Account API Token`.
- Validated production synthetic monitoring after enforced promotion:
  - Run: https://github.com/grigb/universal-manifest/actions/runs/22659519824 (`success`)
  - Synthetic checks + post-deploy verify passed.

Evidence:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-preflight-enabled-success-run-meta.json`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-preflight-enabled-success-run.log`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-preflight-enabled-success-log-extract.txt`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-auth-type-telemetry-success-run-meta.json`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-auth-type-telemetry-success-run.log`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-auth-type-telemetry-success-log-extract.txt`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-api-token-enforcement-success-run-meta.json`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-api-token-enforcement-success-run.log`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-api-token-enforcement-success-log-extract.txt`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-synthetic-prod-post-enforcement-success-run-meta.json`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-synthetic-prod-post-enforcement-success-run.log`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-synthetic-prod-post-enforcement-success-log-extract.txt`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-wo-0124-api-token-enforcement-closeout.md`

## Post-Closeout Addendum (2026-03-05)

Follow-up incident and remediation completed in this pass:
- Production promotion failed on run `22702105155` after token replacement due to missing zone route deploy permission:
  - failure path: Cloudflare API `/zones/.../workers/routes`
  - error: `Authentication error [code: 10000]`
  - production preflight still showed `authType: Account API Token`
- Root cause: production token had valid account auth but insufficient zone route deploy scope.
- User updated Cloudflare token scope to include zone route edit capability, then promotion rerun completed green.

Validation evidence:
- Failed gated run (permission gap): https://github.com/grigb/universal-manifest/actions/runs/22702105155
- Green gated rerun after permission fix: https://github.com/grigb/universal-manifest/actions/runs/22702756070
- Failure meta: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-05-deploy-gated-zone-route-auth-failure-run-meta.json`
- Failure log: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-05-deploy-gated-zone-route-auth-failure-run.log`
- Failure extract: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-05-deploy-gated-zone-route-auth-failure-log-extract.txt`
- Success meta: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-05-deploy-gated-zone-route-auth-remediation-success-run-meta.json`
- Session report: `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-05-wo-0124-cloudflare-token-permission-remediation.md`
