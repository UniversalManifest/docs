# WO-0028 — Astro content-cache duplicate-id warning cleanup and build hardening

**Status:** COMPLETED
**Created:** 2026-02-22

## Objective

Eliminate recurring Astro duplicate-id warning noise caused by stale `.astro` content cache state and make the default site build path deterministic and clean.

## Scope

In scope:
- codify clean-build behavior in default site build command.
- preserve existing dev ergonomics while ensuring CI/local build parity.
- verify a warning-free clean build path with current docs corpus.

Out of scope:
- changing docs content routes or slugs.
- modifying Starlight content model or Astro internals.

## Deliverables

- `/Users/grig/work/repo/universalmanifest/site/package.json`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0028-astro-content-cache-clean-build-hardening.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/workorders/WO-INDEX.md`

## Acceptance criteria

- [x] `npm run build` in `/Users/grig/work/repo/universalmanifest/site` runs with cache cleanup and no duplicate-id warnings.
- [x] `npm run build:clean` remains valid and non-recursive.
- [x] New WO is indexed in both work-order indexes.

## Execution log

Completed changes:
1. Updated `/Users/grig/work/repo/universalmanifest/site/package.json` so default `build` always performs `clean:astro` before sync and Astro build.
2. Simplified `build:clean` to alias `build` (single deterministic clean-build path).
3. Re-ran build commands to confirm warning-free output and valid script wiring.

Validation commands:
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` (pass)
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` (pass)
