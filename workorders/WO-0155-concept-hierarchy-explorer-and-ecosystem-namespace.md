---
status: COMPLETED
created: 2026-03-11T23:00:00Z
updated: 2026-04-01T00:00:00Z
owner: Developer Experience
priority: P0
tags: [concept-explorer, ecosystem, namespace, tooling, adoption]
---

# WO-0155: Concept Hierarchy Explorer and Ecosystem Namespace

## Context

People who encounter Universal Manifest's current documentation tend to over-index on the specific use cases shown (metaverse, smart glasses, galleries, social profiles) and dismiss the project as incomplete or niche. The full conceptual space — every possible application domain, use case, user journey, and integration pattern — is far broader than what any documentation set can cover upfront. Without a way to browse that space, evaluators cannot see the breadth and cannot drill into areas relevant to them.

## Objective

### Immediate Deliverable

Build a single-page HTML/JS concept hierarchy explorer tool that lets people browse the full space of what Universal Manifest can do — organized as an interactive, expandable tree. The tool loads from a JSON data file (`concepts.json`) so the hierarchy can be updated without changing code.

Key requirements:
- Interactive expandable/collapsible tree hierarchy
- Each node shows: name, one-line description, status badge (Proven / Documented / Proposed / Unexplored)
- Click a node for its full description in a detail panel
- Search/filter box to find concepts by keyword
- Dark theme matching the UM site
- Fully self-contained: no CDN, no build step, no npm, no framework dependencies
- Mobile-responsive
- Detail panel shows: description, status, related documents, and "Request Detail" indicator
- JSON is the single source of truth — updating concepts means editing JSON only

### Future Vision (documented, not built in this WO)

1. **On-demand documentation:** Users browse the tree, flag areas they want detail on, and the project team prioritizes explainer/journey creation based on demand signals.

2. **Ecosystem compliance:** External parties can submit compliance documentation to "claim" a namespace in the concept hierarchy — declaring "we implement UM for [this domain]" with verifiable evidence.

3. **Distributed namespace management:** Unique concept/domain names managed by a decentralized solution (not centralized ownership) to prevent namespace squatting while allowing organic growth of the ecosystem registry.

4. **Standards ecosystem:** The hierarchy becomes a living registry of UM application domains with compliance evidence — effectively a directory of who implements what, verified against UM conformance standards.

## Deliverables

- [x] Concept hierarchy JSON data file (`site/public/tools/concept-explorer/concepts.json`) with 150-250 leaf nodes covering all UM application domains
- [x] Single-page interactive explorer (`site/public/tools/concept-explorer/index.html`) with tree view, search, detail panel, and status badges
- [x] Future vision documented in this work order (above)

## Location

`site/public/tools/concept-explorer/`

## Dependencies

- None (standalone tool, no build integration required)
