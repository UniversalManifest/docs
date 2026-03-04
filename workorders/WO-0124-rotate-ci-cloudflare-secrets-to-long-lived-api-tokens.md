# WO-0124 — Rotate CI Cloudflare Secrets to Long-Lived API Tokens

**Status:** IN_PROGRESS
**Created:** 2026-03-04
**Updated:** 2026-03-04
**Priority:** P0
**Owner:** Platform / DevOps
**Source:** Post-WO-0123 durability hardening

## Objective

Replace time-bound Wrangler OAuth-derived CI secrets with long-lived Cloudflare API tokens scoped for staging and production deploy workflows.

## Problem Statement

WO-0123 restored green production promotions using environment-scoped secrets, but the token material currently mirrors local Wrangler OAuth credentials (time-bound access tokens). This can regress when tokens expire.

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

- [ ] Gated production promotion run succeeds after token rotation.
- [ ] Production synthetic monitoring run succeeds after token rotation.
- [ ] No dependence on time-bound OAuth access token material for CI deploys.

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

Evidence:
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-preflight-enabled-success-run-meta.json`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-preflight-enabled-success-run.log`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/operations/2026-03-04-deploy-gated-preflight-enabled-success-log-extract.txt`

Current blocker for completion:
- Long-lived API token issuance could not be completed programmatically from current Wrangler OAuth scopes (no token-management scope available).
- Dashboard automation path is blocked by repeated Cloudflare security challenge in automation context.
