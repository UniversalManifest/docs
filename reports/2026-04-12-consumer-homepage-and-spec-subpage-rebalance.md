# Consumer Homepage and Spec Subpage Rebalance

**Date:** 2026-04-12
**Work order:** [WO-0171 — Consumer-first homepage, spec subpage rebalance, and spec navigation repair](../workorders/WO-0171-consumer-first-homepage-and-spec-subpage-rebalance.md)

## Summary

This implementation rebalanced the public site so the root route is no longer the raw W3C-style specification shell.

Delivered:

- `/` now serves a consumer-first homepage with problem framing, audience lanes, and clear routing into docs, use cases, proof surfaces, and the latest draft specification.
- `/spec/latest/` now serves the current W3C-style specification HTML shell at a stable subordinate route.
- The W3C-style specification shell now includes explicit site navigation so standards readers can move between the homepage, docs, versioned specs, sandbox, and agent-facing surfaces without treating the spec as an isolated homepage.
- The shared public navigation now exposes `Use Cases` and `Latest Spec` directly.
- The curated docs entry now links to the latest draft specification in addition to the versioned spec pages.

## Files Changed

Canonical docs repo:

- `docs/W3C-STYLE-SPEC.html`
- `docs/workorders/WO-0171-consumer-first-homepage-and-spec-subpage-rebalance.md`
- `docs/workorders/WO-INDEX.md`
- `docs/STATE-OF-THE-PROJECT.md`

Parent repo:

- `site/src/pages/index.astro`
- `site/src/pages/spec/latest.astro`
- `site/src/pages/docs/index.astro`
- `site/src/layouts/PublicSurfaceLayout.astro`

## Verification

- `npm run build` in `site/` completed successfully after the route changes.
- The build produced:
  - `/index.html`
  - `/spec/latest/index.html`
  - the existing versioned spec pages under `/spec/v01/` and `/spec/v02/`
- The targeted markdown-link verification for the updated WO/state/index docs returned `TOTAL_MISSING=0`.

## Outcome

The public site now follows the intended outside-in order:

1. Homepage for broad audience comprehension and routing.
2. Curated docs entry for readers who want the corpus.
3. Stable latest-draft spec route for standards readers.
4. Existing versioned spec, proof, integration, and reference routes preserved.
