# WO-0033 — Published docs label-first link normalization

**Status:** COMPLETED  
**Created:** 2026-02-22  
**Priority:** HIGH

## Objective

Normalize published docs so every file/route reference is an actual clickable link with meaningful label-first text, not plain path strings.

## Required output format

Preferred:
- `[Interactive loader (site)](/harness/index.html)`

Accepted equivalent:
- `<a href="/harness/index.html">Interactive loader (site)</a>`

Disallowed:
- `Interactive loader (site): /harness/index.html`
- `Interactive loader (site): <a href="/harness/index.html">/harness/index.html</a>`
- raw path-only bullets with no link text label

## Scope

In scope:
- `/Users/grig/work/repo/universalmanifest/site/src/content/docs/**/*.md`
- Any currently published page under docs content that uses plain route/file path references.

Out of scope:
- code snippets that intentionally demonstrate shell commands.
- normative URI examples used as protocol samples where path is part of sample payload.

## Acceptance criteria

- [x] Every publish-facing route/file reference in docs content is clickable.
- [x] Links use label-first text (not path-as-label unless no meaningful label exists).
- [x] No plain raw route/file references remain in narrative/bulleted reference sections.
- [x] Site build passes.
- [x] Production Pages deploy completed and live checks pass.

## Validation commands

- `rg -n '/[A-Za-z0-9._-]' /Users/grig/work/repo/universalmanifest/site/src/content/docs`
- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- `node /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/build.mjs`
- `CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 npx --yes wrangler pages deploy /Users/grig/work/repo/universalmanifest/deploy/universalmanifest.net/dist --project-name universalmanifest-net --branch main`

## Completion evidence (2026-02-22)

- Normalization scope completed across publish-facing docs in:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/getting-started/*.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/*.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/spec/*.md`
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/publishing/*.md`
- RP1 malformed heading fixed in:
  - `/Users/grig/work/repo/universalmanifest/site/src/content/docs/integrations/rp1-spatial-fabric.md`
- Validation:
  - `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` -> PASS
  - `rg -n '/harness/|/proof/|/getting-started/|/spec/|/conformance/|/workbench/|/integrations/' /Users/grig/work/repo/universalmanifest/site/src/content/docs --glob '*.md' | rg -v '\\]\\([^)]+'` -> no remaining path-only reference hits (except non-path phrase in `conformance/resolver.md`)
- Deploy and live checks:
  - Deploy: `CLOUDFLARE_ACCOUNT_ID=62421a9019bd0761655214e1160bcad0 npx --yes wrangler pages deploy ... --branch main` -> SUCCESS
  - Live `200` checks:
    - `https://universalmanifest.net/`
    - `https://universalmanifest.net/getting-started/workbench/`
    - `https://universalmanifest.net/proof/harness/`
    - `https://universalmanifest.net/integrations/oma-trust/`
    - `https://universalmanifest.net/integrations/rp1-spatial-fabric/`
