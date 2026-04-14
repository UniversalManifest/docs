# WO-0184 -- Static Tool Surface Shell Alignment

**Status:** PLANNED
**Priority:** P1
**Created:** 2026-04-13

## Objective

Bring the remaining raw static tool surfaces into a coherent route/frame strategy without rewriting their internals prematurely.

## Context

The first tool/proof reintegration wave brought `/learning/`, `/sandbox/`, and `/workbench/` into the shared shell family. Remaining static surfaces still feel visually and structurally separate, especially the resolver static UI, concept explorer, harness raw entry, and standalone 404 presentation.

## Scope

In scope:

1. Normalize route-level framing for remaining static tool surfaces.
2. Decide whether each surface should be wrapped, linked as raw payload, or retired.
3. Align 404 and adjacent auxiliary pages with the newer public/tool-shell language where appropriate.

Out of scope:

- major internal rewrites of the tools themselves
- runtime resolver contract changes

## Deliverables

- Shell/framing strategy for resolver static pages, concept explorer, harness raw entry, and 404.
- Implementation pass on the chosen route-level alignment.

## Dependencies

- WO-0183 canonical route and alias policy.

## Acceptance Criteria

- [ ] Remaining static tool surfaces have a deliberate shell strategy.
- [ ] Route-level fragmentation is reduced without destabilizing the raw payloads.
- [ ] 404 and auxiliary static pages no longer feel disconnected from the broader site language.
