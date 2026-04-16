# WO-0186 -- Fixture Mirror Source-of-Truth Consolidation

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13
**Completed:** 2026-04-13

## Objective

Make `examples/` the explicit authored source of truth for fixture data while keeping published fixture copies on the site as generated mirrors for browser tools.

## Context

The project currently serves fixtures from public tool-facing mirrors under `site/public/harness/fixtures/` and `site/public/sandbox/fixtures/`, but authored truth should not drift across multiple trees.

## Scope

In scope:

1. Document and enforce authored fixture truth in `examples/`.
2. Define the generated-mirror relationship for browser-facing site copies.
3. Reduce long-term drift risk between source fixtures and public mirrors.

Out of scope:

- removing browser-accessible fixture copies
- changing conformance semantics

## Deliverables

- Source-of-truth documentation for fixtures.
- Sync/generation policy for published mirrors.
- Implementation pass if tooling updates are needed.

## Completion Notes

- Added the canonical fixture policy document at `docs/FIXTURE-SOURCE-OF-TRUTH-AND-PUBLISHED-MIRROR-POLICY.md`.
- Recorded the docs-side closeout in `docs/reports/2026-04-13-fixture-mirror-source-of-truth-consolidation.md`.
- The paired implementation slice now centralizes fixture mirror definitions in `site/scripts/fixture-mirrors.mjs` and uses that shared model from:
  - `site/scripts/sync-harness-fixtures.mjs`
  - `site/scripts/sync-sandbox-fixtures.mjs`
  - `site/scripts/sync-agent-discovery.mjs`
- The public fixture catalog now exposes authored provenance alongside published paths so generated mirrors are explicit rather than implied.

## Dependencies

- WO-0182 tool/runtime/static boundary decision package.

## Acceptance Criteria

- [x] Authored fixture truth is explicit.
- [x] Published fixture mirrors are documented as generated copies.
- [x] Drift risk between fixture trees is materially reduced.
