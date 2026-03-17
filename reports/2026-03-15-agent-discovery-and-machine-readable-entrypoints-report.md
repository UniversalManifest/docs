# Agent Discovery and Machine-Readable Entry Points Report

**Date:** 2026-03-15
**Related work order:** `WO-0158`
**Status:** Completed first public discovery layer for `universalmanifest.net` and `myum.net`

## Summary

Universal Manifest now exposes a real public discovery layer for both the standards host and the runtime host.

The standards side now publishes:

- `llms.txt`
- `/.well-known/security.txt`
- an enriched `/.well-known/universal-manifest.json`
- a visible `/for-agents/` route in the docs IA
- machine-readable public catalogs for fixtures and sandbox scenarios

The runtime side now publishes:

- `/.well-known/security.txt`
- an enriched `/.well-known/myum-resolver.json`
- `/openapi.json`

This makes the agent entry path explicit and removes the need to scrape browser bundles to discover public fixtures or sandbox routes.

## What Shipped

### Standards host (`universalmanifest.net`)

- Added `site/public/llms.txt`
- Added `site/public/.well-known/security.txt`
- Replaced the minimal `site/public/.well-known/universal-manifest.json` generator with a richer generated descriptor
- Added generated catalogs:
  - `site/public/agent/fixture-catalog.json`
  - `site/public/agent/sandbox-scenarios.json`
- Added `site/src/content/docs/for-agents.md`
- Added `For Agents` to the Starlight sidebar
- Updated `site/src/content/docs/index.md` to route agent readers toward the canonical discovery path

### Runtime host (`myum.net`)

- Added `GET /.well-known/security.txt`
- Added `GET /openapi.json`
- Expanded `GET /.well-known/myum-resolver.json` with discovery and docs links
- Updated resolver docs and runtime contract docs to reflect the new endpoints
- Added contract tests for the new runtime discovery endpoints

## Key Decisions

- Public agent support is currently **read-mostly**.
- `skill.md` is intentionally **deferred**, because these hosts are standards/discovery/runtime surfaces rather than a task-oriented public agent service.
- The standards host and runtime host continue to expose **different but complementary** contracts.

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- `cd /Users/grig/work/repo/universalmanifest/services/myum-resolver && npm test` -> PASS
- `cd /Users/grig/work/repo/universalmanifest/services/myum-resolver && npm run typecheck` -> PASS
- Browser verification against the built site confirmed:
  - `/for-agents/` renders and is linked in the sidebar
  - `/.well-known/universal-manifest.json` is served and includes the new discovery/counter fields

## Remaining Gaps

These are intentionally left to follow-on work orders:

- `WO-0161` implements the landing-first root experience and docs-secondary routing model
- `WO-0159` documents how Universal Manifest should be introduced to external agents in the wild
- `WO-0160` formalizes completeness, anti-fabrication, and verification gates for agent-facing artifacts
