# Remaining Site Build Warning Triage And Noise Reduction

**Date:** 2026-03-17
**Related work order:** `WO-0163`
**Status:** Completed warning triage with two fixes and one intentional acceptance

## Summary

This pass resolved the remaining build-noise debt that was left after `WO-0162`.

Out of the three non-blocking warnings present at the start of the pass:

- two were removed
- one remains and is now explicitly treated as intentional

The result is that the site build no longer emits the sandbox mixed-import warning or the Pagefind `/workbench/index/` warning. The only remaining warning is the known Starlight root-route conflict caused by the deliberate landing-first `/` ownership model.

## Warning Dispositions

### 1. Sandbox mixed static/dynamic import warning

**Previous warning**

Vite warned that `src/scripts/sandbox/scenarios/index.ts` was both dynamically imported and statically imported.

**Root cause**

The sandbox route already statically imported every public scenario module in `src/pages/sandbox/[...scenario].astro`, which meant the client-side lazy-loader path in `src/scripts/sandbox/scenarios/loaders.ts` could not actually create separate chunks.

**Fix**

- removed the unused lazy-loader import from `src/pages/sandbox/[...scenario].astro`
- removed the `await loadScenarioForRoute(...)` call
- deleted `src/scripts/sandbox/scenarios/loaders.ts`

**Disposition**

Fixed.

### 2. Pagefind `/workbench/index/` warning

**Previous warning**

Pagefind reported that `/workbench/index/` had no outer `<html>` element and skipped indexing it.

**Root cause**

The warning came from the Astro-config redirect for `/workbench/index`, which generated `dist/workbench/index/index.html` as a minimal redirect stub without a full `<html>` root.

**Fix**

- removed the `redirects` entry from `site/astro.config.mjs`
- added an explicit redirect page at `site/src/pages/workbench/index/index.astro` with a full HTML document

**Disposition**

Fixed.

### 3. Starlight `/` route-priority warning

**Current warning**

Starlight still warns that the docs router cannot render its empty-slug route because the custom `/` route has higher priority.

**Reason**

This is the intended result of the landing-first public-surface model introduced in `WO-0161`. The public root is now owned by `site/src/pages/index.astro`, while the documentation system still contains a docs-root entry under `site/src/content/docs/index.md`.

**Disposition**

Intentionally retained and accepted for now. Removing it would require changing the docs-root content strategy rather than simply suppressing a build warning. That is broader than this warning-reduction pass.

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- The sandbox mixed-import warning is gone
- The Pagefind `/workbench/index/` no-outer-`<html>` warning is gone
- The only remaining build warning is:
  - `Could not render `` from route /[...slug] as it conflicts with higher priority route /`
- Served-route checks returned `200 OK` for:
  - `/workbench/`
  - `/workbench/index/`
  - `/sandbox/gs-01-first-manifest-v2/`

## Browser Verification Note

I did not complete a fresh browser-MCP verification pass in this session because the browser transports were unavailable earlier in the same session. Verification for this work therefore relied on the successful site build plus direct served-route checks against the built output.

## Result

`WO-0163` is complete. The site build warning baseline is now accurate: one intentional Starlight root-route warning remains, and the two previously noisy structural warnings have been removed.
