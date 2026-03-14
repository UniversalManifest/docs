# WO-0023 — Production deployment drift prevention automation

**Status:** COMPLETED  
**Created:** 2026-02-20

## Objective

Reduce drift between repository `main` and production endpoints with a repeatable post-deploy verification workflow.

## Scope

In scope:
- define and implement a post-deploy verification routine for critical docs/resolver routes.
- add an auditable report artifact path for each deploy cycle.
- ensure route checks include:
  - workbench docs/tool routes
  - resolver health and well-known endpoint
  - resolver host variant (`www.myum.net`) coverage
- update deployment docs/runbooks with the automation commands.

Out of scope:
- replacing existing hosting providers or changing domain architecture.

## Deliverables

- script/runbook updates under:
  - `deploy/`
  - `docs/`
  - `packages/universal-manifest/scripts/`
- deployment verification report template/artifacts under:
  - `.dev/ai/reports/`

## Acceptance criteria

- [x] one command sequence performs route + contract verification after deploy.
- [x] verification includes both `universalmanifest.net` workbench paths and `myum.net`/`www.myum.net` resolver health.
- [x] results are saved to a timestamped report artifact path.
- [x] documented process is reproducible by a zero-context operator.

## Dependencies

- `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
- `services/myum-resolver/CLOUDFLARE-DEPLOY.md`
- `docs/reports/2026-02-20-master-forward-worklist.md`

## Completion evidence (2026-02-20)

- Automation script:
  - `packages/universal-manifest/scripts/post-deploy-verify.mjs`
- npm command:
  - `cd packages/universal-manifest && npm run verify:postdeploy:prod`
- report artifact (PASS):
  - `.dev/ai/reports/deploy-checks/2026-02-20T05-44-07-832Z-post-deploy-verification.md`
- runbook updates:
  - `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
  - `services/myum-resolver/CLOUDFLARE-DEPLOY.md`
