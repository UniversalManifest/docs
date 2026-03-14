# WO-0123 — Cloudflare Credential Stabilization for Gated Production Promotions

**Status:** COMPLETED
**Created:** 2026-03-04
**Updated:** 2026-03-04
**Priority:** P0
**Owner:** Platform / DevOps
**Source:** Repeated production deploy failures in gated promotions despite runtime health

## Objective

Eliminate Cloudflare credential/rate-limit instability in CI promotions so `Deploy (Gated)` production path can complete reliably without manual fallback deploys.

## Problem Statement

Current production promotion runs repeatedly fail in `deploy_production_resolver` with Cloudflare API errors (`10429`, `10000`, `9109`).

Workflow and sequencing hardening is now in place and validated, but credential reliability remains a platform blocker.

## Scope

In scope:
- create/assign dedicated staging and production Cloudflare API tokens
- set GitHub environment secrets for staging/production credential isolation
- run gated deployment validations to confirm production resolver+docs deploy success
- capture evidence and close WO upon two consecutive green production promotions

Out of scope:
- resolver contract changes
- frontend/UI changes
- unrelated docs restructure

## Deliverables

1. Cloudflare one-time token setup completed for staging and production scopes.
2. GitHub environment secrets populated:
- `CF_ACCOUNT_ID_STAGING`
- `CF_API_TOKEN_STAGING`
- `CF_ACCOUNT_ID_PRODUCTION`
- `CF_API_TOKEN_PRODUCTION`
3. At least two successful `Deploy (Gated)` runs with `promote_to_production=true`.
4. Updated operational evidence report and WO closure note.

## Acceptance Criteria

- [x] `Deploy (Gated)` production promotion run completes with production resolver job `success`.
- [x] Production docs job `success` in same run.
- [x] Production verify gates job `success` in same run.
- [x] Second consecutive production promotion run also green.
- [x] Evidence paths and run URLs appended to operations report and WO-INDEX status updated to COMPLETED.

## Dependencies

- `.github/workflows/deploy-gated.yml`
- `.dev/ai/reports/operations/2026-03-04-cloudflare-one-time-setup-checklist-for-gated-deploy.md`
- GitHub repo: `grigb/universal-manifest`
- Cloudflare account access for token creation and scope assignment

## Current Evidence Snapshot

- Hardening validation summary:
  - `.dev/ai/reports/operations/2026-03-04-deploy-gated-hardening-validation-summary.md`
- Latest sequential-staging production attempt (failed at production resolver):
  - https://github.com/grigb/universal-manifest/actions/runs/22657904731
- Manual production recovery and runtime health evidence:
  - `.dev/ai/reports/operations/2026-03-04-production-promotion-failure-and-manual-recovery-summary.md`
  - `.dev/ai/reports/operations/2026-03-04-post-hardening-final-post-deploy-verification.md`

## Completion Evidence (2026-03-04)

Credential setup + two consecutive green production promotions:
- Run 1 (green): https://github.com/grigb/universal-manifest/actions/runs/22658547313
- Run 2 (green): https://github.com/grigb/universal-manifest/actions/runs/22658652963

Closeout report:
- `.dev/ai/reports/operations/2026-03-04-wo-0123-credential-stabilization-closeout.md`

Run artifacts:
- `.dev/ai/reports/operations/2026-03-04-deploy-gated-credential-stabilization-success-run1-meta.json`
- `.dev/ai/reports/operations/2026-03-04-deploy-gated-credential-stabilization-success-run1.log`
- `.dev/ai/reports/operations/2026-03-04-deploy-gated-credential-stabilization-success-run2-meta.json`
- `.dev/ai/reports/operations/2026-03-04-deploy-gated-credential-stabilization-success-run2.log`

Post-closeout synthetic confirmation:
- https://github.com/grigb/universal-manifest/actions/runs/22658785827 (`success`)
- `.dev/ai/reports/operations/2026-03-04-post-wo0123-synthetic-prod-green-run-meta.json`
