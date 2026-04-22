# WO-0185 -- Latest Spec Surface Strategy and Shell Implementation

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13
**Completed:** 2026-04-22

## Objective

Decide and implement the long-term architectural model for `/spec/latest/` so the latest specification is both standards-reader-friendly and structurally consistent with the rest of the public site.

## Context

`/spec/latest/` is still the clearest remaining legacy fragment. It is important and public, but it relies on injected checked-in HTML rather than the broader shell model now used elsewhere.

## Scope

In scope:

1. Decide whether the injected W3C-style shell remains the permanent model.
2. If not, define the migration approach that preserves standards-reader expectations.
3. Implement the chosen route/shell strategy without making the spec harder to reach or read.

Out of scope:

- changing the normative meaning of the spec
- widening the primary public menu

## Deliverables

- Decision package for the `/spec/latest/` architecture.
- Implementation pass on the approved shell strategy.

## Completion Notes

- Chosen durable model: keep `/spec/latest/` as a dedicated W3C-style standards-reader surface, but move route-shell ownership into Astro instead of continuing to inject a full standalone HTML document verbatim.
- `site/src/pages/spec/latest.astro` now extracts the checked-in spec document's head/body markup, emits the canonical page shell for `/spec/latest/`, and keeps internal public links host-relative.
- `docs/W3C-STYLE-SPEC.html` remains the source of truth for the specification body, W3C reader styling, and TOC behavior, but it no longer owns the site navigation for the route.
- Recorded the closeout and verification evidence in `docs/reports/2026-04-22-latest-spec-surface-strategy-and-shell-implementation.md`.

## Dependencies

- WO-0183 canonical route and compatibility alias policy.

## Acceptance Criteria

- [x] `/spec/latest/` has a documented long-term architectural model.
- [x] The resulting surface preserves easy public access to the latest spec.
- [x] The implementation no longer feels like an unresolved structural exception.
