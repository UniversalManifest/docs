# WO-0257: GitHub Actions Submodule Checkout Deploy Build Unblock

**Status:** COMPLETED 2026-05-02
**Priority:** P0 (blocks deployment verification)
**Depends on:** WO-0254
**Unblocks:** WO-0255
**Derived from:** 2026-05-02 GitHub Actions build failure after WO-0254 push

## Problem

After `WO-0254` was committed and pushed, GitHub Actions build jobs failed because the Astro page at `/spec/latest/` imports the raw W3C-style specification HTML from the repository's `docs` submodule:

`/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html`

The local checkout has `docs` initialized, but GitHub Actions default checkout does not initialize submodules unless requested. As a result, site/deploy jobs can fail before a production deploy happens, leaving the public routes `/spec/latest/`, `/spec/v0.2/`, `/explorer/`, `/how-it-works/`, and `/standards-fit/` on the previously deployed 404 state.

`WO-0255` cannot verify production reader routes until the pushed ref can build and deploy.

## Objective

Unblock GitHub Actions site and deploy builds by ensuring the workflows that build the Astro site initialize the `docs` submodule before running the build.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/spec/latest.astro`
- `/Users/grig/work/repo/universalmanifest/.gitmodules`

## Work to perform

1. Update the `build_publish_bundle` checkout in `deploy-gated.yml` so it fetches submodules before the Astro build.
2. Update the `verify.yml` checkout for its docs-site build so it fetches submodules.
3. Update the `ci.yml` `build-site` job checkout so it fetches submodules.
4. Run YAML syntax/format sanity checks if available, or inspect the patched snippets.
5. Commit and push the docs submodule update to `upstream/main`.
6. Commit and push the parent repo workflow/submodule-pointer update to `origin/main`.

## Files expected to modify

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0257-github-actions-submodule-checkout-deploy-build-unblock.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml`
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml`

## Constraints

- Do not modify site implementation files.
- Do not change normative specification content.
- Do not broaden scope into conformance or terminology failures unless they directly prevent the deploy-gated build from starting.
- Do not deploy from this work order.

## Acceptance criteria

- GitHub Actions site/deploy build checkouts initialize the `docs` submodule where needed.
- The deploy-gated build should be able to access `/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html` during Astro build.
- Local YAML syntax/format sanity is completed or the patched snippets are manually inspected.
- Docs submodule updates are pushed to `upstream/main`.
- Parent repo updates are pushed to `origin/main`.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-05-02-wo-0257-result.md`

## Closeout Evidence

Workflow patches completed:

- `/Users/grig/work/repo/universalmanifest/.github/workflows/deploy-gated.yml` — `build_publish_bundle` checkout now fetches submodules before `npm run build:clean`.
- `/Users/grig/work/repo/universalmanifest/.github/workflows/verify.yml` — docs-site build checkout now fetches submodules before `npm run build`.
- `/Users/grig/work/repo/universalmanifest/.github/workflows/ci.yml` — `build-site` checkout now fetches submodules before `npm run build:clean`.

Verification completed:

- `/Users/grig/work/repo/universalmanifest/docs/W3C-STYLE-SPEC.html` exists in the initialized local submodule.
- `ruby -e 'require "yaml"; ARGV.each { |f| YAML.load_file(f); puts "OK #{f}" }' .github/workflows/deploy-gated.yml .github/workflows/verify.yml .github/workflows/ci.yml` passed.
- `actionlint -shellcheck= -pyflakes= .github/workflows/deploy-gated.yml .github/workflows/verify.yml .github/workflows/ci.yml` passed.
- `npm run build:clean` passed from `/Users/grig/work/repo/universalmanifest/site` and generated `/spec/latest/`, `/spec/v0.2/`, `/explorer/`, `/how-it-works/`, and `/standards-fit/` locally.

No deploy was run in this work order.
