# WO-0184 -- Static Tool Surface Shell Alignment

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13
**Completed:** 2026-04-22

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

## Completion Notes

- Closed the docs-side slice against the verified clean-branch implementation for `WO-0184`.
- Route/shell alignment now covers `/404.html`, `/proof/harness/`, `/resolver/`, `/resolver/ops/`, `/resolver/result/`, and `/tools/concept-explorer/`.
- Raw payloads remain preserved behind subordinate app paths where needed, including `/resolver/app/` and `/tools/concept-explorer/app/`, so the route framing changed without rewriting the underlying tool payloads.
- Build passed for the paired implementation slice, and browser verification was clean for `/404.html`, `/proof/harness/`, `/resolver/`, and `/tools/concept-explorer/` after fixing the concept explorer payload path.
- Recorded the docs closeout in `docs/reports/2026-04-22-static-tool-surface-shell-alignment-closeout.md`.

## Dependencies

- WO-0183 canonical route and alias policy.

## Acceptance Criteria

- [x] Remaining static tool surfaces have a deliberate shell strategy.
- [x] Route-level fragmentation is reduced without destabilizing the raw payloads.
- [x] 404 and auxiliary static pages no longer feel disconnected from the broader site language.
