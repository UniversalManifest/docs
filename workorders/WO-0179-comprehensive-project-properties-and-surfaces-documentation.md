# WO-0179 -- Comprehensive Project, Property, and Surface Documentation

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-13

## Objective

Create one canonical documentation file that maps the entire Universal Manifest project across repo areas, public properties, route families, tool/proof surfaces, runtime surfaces, and governance/source-of-truth boundaries.

## Context

The repo had enough surface area that high-level status documents and route-specific docs were no longer sufficient on their own. A deeper, single-file structural map was needed so a human or agent could understand the whole system without reconstructing it from multiple partial documents.

## Scope

In scope:

1. Create a full project/property/surface map.
2. Make the document reachable from the canonical docs index.
3. Record the deliverable in the formal work-order ledger.
4. Sync the mirrored knowledge layer.

Out of scope:

- changing route behavior
- changing runtime behavior
- redesigning any public surface

## Deliverables

- Canonical comprehensive map:
  - `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
- Docs-index integration:
  - `docs/README.md`
- Knowledge-pointer integration:
  - `docs/PROJECT-KNOWLEDGE-INDEX.md`

## Completion Notes

- Added a single-file architecture map covering:
  - repo ownership by major area
  - `universalmanifest.net` surface families
  - `myum.net` runtime surfaces
  - `site/src/pages`, `site/src/content/docs`, and `site/public` families
  - source-of-truth ownership across standard, site, runtime, governance, and mirror layers
- Updated the canonical docs index so the map is reachable from the primary documentation entry point.
- Updated the knowledge-pointer layer so the map is part of the recommended local-first reading order.

## Acceptance Criteria

- [x] A single canonical project/property/surface map exists.
- [x] The docs index points to it.
- [x] The knowledge-pointer layer includes it in the reading order.
- [x] The formal work-order ledger records the deliverable.
