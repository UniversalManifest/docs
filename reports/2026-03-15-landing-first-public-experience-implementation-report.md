# Landing-First Public Experience Implementation Report

**Date:** 2026-03-15
**Related work order:** `WO-0161`
**Status:** Completed landing-first root experience and secondary docs entry path

## Summary

Universal Manifest now has a real public landing page at `/` and a dedicated documentation entry at `/docs/`.

This changes the site posture from "docs shell that happens to be public" to "public landing surface that routes people and agents into the right layer." The docs corpus remains intact, but it is no longer forced to serve as the first thing every visitor sees.

## What Shipped

### Public landing surface

- Added `site/src/pages/index.astro`
- Added `site/src/layouts/PublicSurfaceLayout.astro`
- Added `site/src/styles/public-surface.css`
- Introduced explicit primary navigation for:
  - Home
  - Docs
  - Agents
  - Sandbox
  - Harness
  - Resolver
- Added audience lanes for:
  - evaluators
  - implementers
  - agents
  - proof/tool explorers

### Secondary docs entry

- Added `site/src/pages/docs/index.astro`
- Updated `site/astro.config.mjs` so the docs sidebar now treats `/docs/` as the curated documentation start
- Updated discovery metadata so the standards descriptor points at `/` as landing and `/docs/` as the documentation home
- Updated `site/public/llms.txt` to reflect the landing/docs split

### Compatibility posture

- Existing deep content routes under `/about/`, `/getting-started/`, `/spec/`, `/reference/`, `/integrations/`, `/proof/`, and `/governance/` remain intact
- The landing page is directional rather than duplicating the docs corpus
- The docs entry page is curated rather than replacing the existing published routes

## Key Decisions

- `/` is now the public front door, not the docs homepage
- `/docs/` is the canonical "start here" path for documentation readers
- The landing experience is intentionally short and routing-oriented
- The standards host continues to own landing, docs, discovery, tools, and artifacts, while `myum.net` stays the runtime/resolver host

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- Browser verification confirmed:
  - `/` renders the new landing page and audience lanes
  - `/docs/` renders the new curated docs entry page
  - existing deep route `/about/agent-briefing/` still loads

## Known Warnings

- Astro reports an expected route-priority warning because the new custom `/` page intentionally supersedes the old Starlight root docs route
- Existing sandbox chunk-size and workbench Pagefind warnings remain and predate this work order
