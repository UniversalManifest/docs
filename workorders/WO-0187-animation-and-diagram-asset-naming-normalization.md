# WO-0187 -- Animation and Diagram Asset Naming Normalization

**Status:** PLANNED
**Priority:** P2
**Created:** 2026-04-13

## Objective

Normalize the naming conventions for public animation and diagram assets while preserving external-link continuity where needed.

## Context

The public asset libraries are valuable and should remain published, but they carry duplicate naming schemes from multiple execution waves. That makes long-term maintenance and linking less coherent than it should be.

## Scope

In scope:

1. Establish canonical naming rules for animation and diagram assets.
2. Identify which existing names must remain as aliases for continuity.
3. Update documentation and asset references accordingly.

Out of scope:

- redesigning the assets themselves
- deleting externally referenced files without continuity planning

## Deliverables

- Canonical naming policy.
- Asset rename/alias plan.
- Implementation pass on the highest-value normalization slice.

## Dependencies

- WO-0183 canonical route and compatibility alias policy.

## Acceptance Criteria

- [ ] Asset naming has a canonical convention.
- [ ] Backward-compatibility needs are documented.
- [ ] Future asset publication no longer compounds naming drift.
