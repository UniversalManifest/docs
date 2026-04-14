# WO-0186 -- Fixture Mirror Source-of-Truth Consolidation

**Status:** PLANNED
**Priority:** P1
**Created:** 2026-04-13

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

## Dependencies

- WO-0182 tool/runtime/static boundary decision package.

## Acceptance Criteria

- [ ] Authored fixture truth is explicit.
- [ ] Published fixture mirrors are documented as generated copies.
- [ ] Drift risk between fixture trees is materially reduced.
