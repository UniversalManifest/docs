# WO-0255: Public Route and Deployment Verification for v0.2 Reader Path

**Status:** BLOCKED 2026-05-02 — Cloudflare deployment credentials in GitHub Actions are invalid, so the redesigned site cannot be deployed to staging/production for public route verification
**Priority:** P0 (blocks external-reader validation)
**Depends on:** WO-0254
**Unblocks:** WO-0256
**Derived from:** 2026-05-02 objective realignment; production-route mismatch observed during local review

## Problem

Local routes were verified during the homepage review, but production v0.2 reader routes were observed returning `404` on 2026-05-01 for `/spec/latest/` and `/spec/v0.2/`.

External-reader validation cannot proceed against a public standard experience if critical public routes fail or drift from the local build.

## Current blocker

`WO-0254` implementation is committed and pushed, and `WO-0257` fixed the GitHub Actions submodule checkout/build blocker. `WO-0258` then repaired the remaining CI/deploy gate drift: `verify` passed at `https://github.com/grigb/universal-manifest/actions/runs/25253951175`, and `CI/CD Pipeline` passed at `https://github.com/grigb/universal-manifest/actions/runs/25253951171`.

The latest gated deploy run at `https://github.com/grigb/universal-manifest/actions/runs/25253991767` built the publish bundle successfully, then stopped at `Deploy staging resolver` during Cloudflare auth preflight:

- staging resolver deploy: `Invalid access token [code: 9109]`

The older gated deploy run at `https://github.com/grigb/universal-manifest/actions/runs/25244375424` also showed the same credential failure before updating staging:

- staging resolver deploy: `Invalid access token [code: 9109]`
- staging docs deploy: `Invalid access token [code: 9109]`

Repository secrets currently include `CF_ACCOUNT_ID` and `CF_API_TOKEN`, but the configured `CF_API_TOKEN` is not accepted by Cloudflare. Until the Cloudflare token is rotated or replaced in GitHub repository secrets, production cannot be updated and this WO cannot verify the redesigned public route path. The workflow now fails directly at the deploy step instead of continuing into stale staging verification.

Direct public checks after the 2026-05-02 14:21 UTC failed deploy still show the old route state:

- `https://universalmanifest.net/` -> `200`
- `https://universalmanifest.net/use-cases/` -> `200`
- `https://universalmanifest.net/explorer/` -> `404`
- `https://universalmanifest.net/how-it-works/` -> `404`
- `https://universalmanifest.net/standards-fit/` -> `404`
- `https://universalmanifest.net/spec/latest/` -> `404`
- `https://universalmanifest.net/spec/v0.2/` -> `404`
- `https://universalmanifest.net/guides/migration-v01-v02/` -> `200`
- `https://universalmanifest.net/publishing/changelog/` -> `200`
- `https://universalmanifest.net/.well-known/universal-manifest.json` -> `200`
- `https://universalmanifest.net/llms.txt` -> `200`

## Objective

Verify the production reader path for the homepage cluster and v0.2 publication surfaces after the approved redesign is implemented and deployed.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/docs/PUBLISHING-AND-VERSIONING.md`
- `/Users/grig/work/repo/universalmanifest/docs/reports/2026-04-30-v0-2-publication-evidence-pack.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0254-implement-approved-homepage-cluster-redesign.md`
- `/Users/grig/work/repo/universalmanifest/site/src/pages/`
- `/Users/grig/work/repo/universalmanifest/site/public/.well-known/universal-manifest.json`
- `/Users/grig/work/repo/universalmanifest/site/public/llms.txt`

## Work to perform

1. Verify the public homepage cluster routes:
   - `https://universalmanifest.net/`
   - `https://universalmanifest.net/use-cases/`
   - `https://universalmanifest.net/explorer/`
   - `https://universalmanifest.net/how-it-works/`
   - `https://universalmanifest.net/standards-fit/`
2. Verify the v0.2 publication-reader routes:
   - `https://universalmanifest.net/spec/latest/`
   - `https://universalmanifest.net/spec/v0.2/`
   - `https://universalmanifest.net/guides/migration-v01-v02/`
   - `https://universalmanifest.net/publishing/changelog/`
3. Verify machine-readable discovery:
   - `https://universalmanifest.net/.well-known/universal-manifest.json`
   - `https://universalmanifest.net/llms.txt`
4. Check that the public pages expose the approved design and current v0.2 posture.
5. Convert any failed route or drift into a follow-on implementation/deploy fix before reader validation proceeds.

## Files to modify / create

- Create `/Users/grig/work/repo/universalmanifest/docs/reports/{date}-v0-2-reader-path-production-verification.md`
- Optional follow-on WO files only if production failures are found.

## Constraints

- Do not treat local `200` checks as production verification.
- Do not run reader validation while required production routes fail.
- Do not reintroduce deleted workflow automation as part of this WO.
- Do not modify spec content.

## Acceptance criteria

- Every required production route returns `200`.
- The production homepage cluster visibly reflects the approved redesign.
- The latest spec and durable v0.2 spec are both reachable.
- Discovery descriptor and `llms.txt` are reachable and reference the current published posture.
- A verification report records exact URLs, status codes, timestamps, and any failures.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0255-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0255-BLOCKED.md`
