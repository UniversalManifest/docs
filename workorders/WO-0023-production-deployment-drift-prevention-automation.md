# WO-0023 — Production deployment drift prevention automation

**Status:** NOT_STARTED  
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
  - `/Users/grig/work/repo/universalmanifest/deploy/`
  - `/Users/grig/work/repo/universalmanifest/docs/`
  - `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/`
- deployment verification report template/artifacts under:
  - `/Users/grig/work/repo/universalmanifest/.dev/ai/reports/`

## Acceptance criteria

- [ ] one command sequence performs route + contract verification after deploy.
- [ ] verification includes both `universalmanifest.net` workbench paths and `myum.net`/`www.myum.net` resolver health.
- [ ] results are saved to a timestamped report artifact path.
- [ ] documented process is reproducible by a zero-context operator.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/CLOUDFLARE-DEPLOY.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-02-20-master-forward-worklist.md`

