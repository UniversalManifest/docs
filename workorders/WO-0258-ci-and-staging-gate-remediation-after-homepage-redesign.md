# WO-0258: CI and Staging Gate Remediation After Homepage Redesign

**Status:** IN_PROGRESS 2026-05-02
**Priority:** P0 (blocks WO-0255 production verification)
**Depends on:** WO-0254, WO-0257
**Unblocks:** WO-0255
**Derived from:** 2026-05-02 GitHub Actions failures after homepage cluster redesign deployment attempt

## Problem

After `WO-0257` restored submodule checkout for site builds, the deploy-gated workflow progressed past build and staging deploy, but verification still failed. The current failures are not homepage design defects; they are gate/contract drift that prevents the redesigned public surface from being deployed and verified:

- CI terminology check rejects first-read documentation wording in `site/src/content/docs/index.md`.
- Route artifact checks still assume `/sandbox/test/` emits `sandbox/test/index.html`, while the Astro build emits a compatible static artifact at a different path.
- Link checking follows absolute `https://universalmanifest.net/...` self-links against production before the new routes have been deployed, causing expected new local routes to fail as production 404s.
- Staging smoke verification reports the resolver response does not expose the full required resolver header contract.

`WO-0255` cannot be completed until the CI and staging gates are green enough to deploy and verify production routes.

## Objective

Restore the CI and deploy-gated verification path so the already-implemented homepage cluster can be promoted to production and publicly verified.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `/Users/grig/work/repo/universalmanifest/services/myum-resolver/src/index.ts`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`

## Work to perform

1. Fix first-read terminology violations without weakening the terminology guardrail.
2. Fix route artifact verification so it matches actual static output while still proving required tool routes exist.
3. Fix CI link checking so pre-deploy builds are checked against local output instead of stale production self-links.
4. Diagnose and repair the staging resolver header-contract failure or accurately reclassify it if it is external-only.
5. Run local verification commands for affected workflows/scripts.
6. Commit and push docs submodule changes to `upstream/main`.
7. Commit and push parent repository changes to `origin/main`.
8. Re-run the gated deploy and resume `WO-0255` if gates pass.

## Files expected to modify

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0258-ci-and-staging-gate-remediation-after-homepage-redesign.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/index.md`
- Additional files only if required by the resolver-header investigation.

## Constraints

- Do not redesign the homepage in this work order.
- Do not weaken required resolver contract assertions.
- Do not hide broken external links broadly; scope link-check changes to the pre-deploy self-link mismatch.
- Do not simulate external reader validation.

## Acceptance criteria

- Terminology check passes.
- Route artifact checks pass against the actual Astro output.
- Link checks no longer fail solely because new local routes are not yet deployed to production.
- Staging resolver header-contract smoke test passes, or a true external blocker is documented with evidence.
- `WO-0255` can be resumed after a successful deploy-gated run.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-05-02-wo-0258-result.md`
