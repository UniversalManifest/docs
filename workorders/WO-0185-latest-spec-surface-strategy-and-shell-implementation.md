# WO-0185 -- Latest Spec Surface Strategy and Shell Implementation

**Status:** PLANNED
**Priority:** P1
**Created:** 2026-04-13

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

## Dependencies

- WO-0183 canonical route and compatibility alias policy.

## Acceptance Criteria

- [ ] `/spec/latest/` has a documented long-term architectural model.
- [ ] The resulting surface preserves easy public access to the latest spec.
- [ ] The implementation no longer feels like an unresolved structural exception.
