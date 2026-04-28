# WO-0227: Post-Publish Smoke — CI-Runnable Production Smoke Harness

**Status:** OBSOLETE 2026-04-28 — was scoped to live inside `.github/workflows/publish-spec.yml`, which was removed in revert commit `e493b3e`. If a manual `npm run smoke:publication` script is wanted, scope a fresh WO; do not resurrect this one.
**Priority:** P0 (verifies publication success in production)
**Depends on:** WO-0222
**Unblocks:** WO-0229
**Derived from:** 2026-04-26 v0.2 publication push plan, item 7; `docs/PUBLISHING-AND-VERSIONING.md` §8 (release-readiness checklist); existing `packages/universal-manifest/scripts/smoke-endpoints.mjs`

## Objective

Define and add a CI-runnable smoke check that verifies in production: (a) `/spec/latest/` and `/spec/v0.2/` both return 200; (b) the published spec body declares published-not-draft status; (c) the JSON-LD context and JSON Schema URLs return correct content types AND immutability headers; (d) the well-known descriptor declares v0.2 as `stable`; (e) the migration-guide and governance links from the spec page return 200; (f) no broken links in the migration / governance docs.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/packages/universal-manifest/scripts/smoke-endpoints.mjs`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/phase-9-gate.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/synthetic-monitoring.yml`
- `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md` §8
- `/Users/grig/work/repo/universalmanifest/docs/RELEASING.md` §3.2

## Work to perform

1. **Extend `packages/universal-manifest/scripts/smoke-endpoints.mjs`** (or add a sibling `smoke-publication.mjs` if extending feels overloaded) to assert:
   - `GET https://universalmanifest.net/spec/latest/` → 200 AND body contains "v0.2 Specification" (no "Draft Specification")
   - `GET https://universalmanifest.net/spec/v0.2/` → 200 (durable URL)
   - `HEAD https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld` → 200, Content-Type contains `ld+json`, Cache-Control contains `immutable` or `max-age=31536000`
   - `HEAD https://universalmanifest.net/ns/universal-manifest/v0.2/schema.json` → 200, Content-Type contains `schema+json` or `application/json`
   - `GET https://universalmanifest.net/.well-known/universal-manifest.json` → 200 AND `versions.stable === "v0.2"` AND `currentSpecVersion === "v0.2"`
   - `GET https://universalmanifest.net/conformance/v0.2/` → 200
   - `GET https://universalmanifest.net/governance/breaking-change-policy/` → 200
   - Migration guide URL → 200
2. **Add an npm script** in `packages/universal-manifest/package.json`: `smoke:publication`.
3. **Wire into CI:** add a job to `.github/workflows/verify.yml` (or create `.github/workflows/post-publish-smoke.yml`) that runs `smoke:publication` on push-to-main AND on a daily cron. The job MUST set its own threshold for "fail loudly" — any single assertion failing fails the job.
4. **Run the harness against staging first** (per `docs/site/STAGING-PROMOTION-RUNBOOK.md` if applicable) and confirm it passes before promoting to production.
5. **Document the harness** in `docs/PRODUCTION-DEPLOY-SMOKE.md`.

## Files to modify

- `packages/universal-manifest/scripts/smoke-endpoints.mjs` (extend) OR `packages/universal-manifest/scripts/smoke-publication.mjs` (new)
- `packages/universal-manifest/package.json` (add `smoke:publication` script)
- `.github/workflows/verify.yml` OR new `.github/workflows/post-publish-smoke.yml`
- `docs/PRODUCTION-DEPLOY-SMOKE.md` (extend the documented runbook)

## Constraints

- **No flaky assertions.** Network calls retry up to 3 times with exponential backoff.
- **No private credentials.** All assertions are against public unauthenticated endpoints.
- **CI runtime budget < 90 seconds** for the smoke job.
- **Failure mode:** when the smoke fails, the job exits non-zero AND posts the failing assertion's details. No silent failures.

## Acceptance criteria

- `npm run smoke:publication` executes locally against production and exits 0 (after WO-0222 lands and production deploy completes).
- The CI job runs on push-to-main and on a daily cron.
- Each of the eight assertions listed in step 1 is implemented.
- `docs/PRODUCTION-DEPLOY-SMOKE.md` documents the new harness and the expected outputs.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0227-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0227-BLOCKED.md`
