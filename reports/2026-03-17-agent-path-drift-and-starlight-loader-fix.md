# Agent Path Drift And Starlight Loader Fix

**Date:** 2026-03-17
**Related work order:** `WO-0162`
**Status:** Completed authority-doc reconciliation and resolved the Starlight duplicate-id warning

## Summary

The remaining cleanup work on the new agent-facing path is now closed.

Two things happened in this pass:

- the older authority documents were reconciled to the new landing/docs/discovery/runtime split
- the Starlight duplicate-id warning was traced to an outdated content-collection configuration and resolved by switching the docs collection to `docsLoader()`

The public `/for-agents/` path and related routes remained stable throughout.

## Root Cause

The duplicate-id warning initially looked like a markdown-slug collision on the changed docs pages. That turned out to be misleading.

The actual issue was that the site was on a Starlight/Astro version combination that expects the docs content collection to use `docsLoader()`. The project was still configured with only:

`defineCollection({ schema: docsSchema() })`

After updating `site/src/content.config.ts` to:

- import `docsLoader` from `@astrojs/starlight/loaders`
- add `loader: docsLoader()` to the `docs` collection

the duplicate-id warning disappeared on the next build.

## What Changed

### Doc drift reconciliation

The authority and boundary documents now consistently describe:

- the landing-first `/` surface
- `/docs/` as the secondary documentation entry
- `/for-agents/` and `/for-agents/external-agent-onboarding/` as the public agent path
- the split between `universalmanifest.net` as standards/discovery/tooling and `myum.net` as the runtime resolver host

### Build warning resolution

The site content configuration now uses the Starlight docs loader expected by the installed version:

- `site/src/content.config.ts`

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- The prior Starlight `glob-loader` duplicate-id warning no longer appears in build output
- Served-route checks returned `200 OK` for:
  - `/for-agents/`
  - `/for-agents/external-agent-onboarding/`
  - `/about/agent-briefing/`
  - `/publishing/domain-split/`

## Remaining Warnings

The build is now clear of the duplicate-id issue. The remaining warnings are pre-existing and non-blocking:

- Vite warning about mixed static and dynamic imports in `src/scripts/sandbox/scenarios/index.ts`
- Intentional Starlight route-priority warning because the custom landing page owns `/`
- Pagefind warning that `/workbench/index/` has no outer `<html>` element

## Browser Verification Note

I attempted a fresh browser-MCP verification pass for the affected routes, but both browser transports were unavailable during this session (`chrome-devtools` and `playwright-codex` returned transport-closed errors). I therefore limited route verification to the successful site build plus direct served-route checks.

## Result

`WO-0162` is complete. The agent-facing path is now coherent in the docs layer, and the Starlight loader mismatch that was producing false duplicate-id noise is resolved.
