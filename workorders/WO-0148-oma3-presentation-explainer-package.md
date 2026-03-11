---
status: COMPLETED
created: 2026-03-11T20:30:00Z
updated: 2026-03-11T20:45:00Z
owner: Standards Alignment
priority: P0 (OMA3 presentation is 2026-03-12)
tags: [oma3, presentation, explainer, iwps, architectural-overview]
---

# WO-0148: OMA3 Presentation Explainer Package

## Context

Tomorrow (2026-03-12) there is a presentation to OMA3 (specifically to Alfred Tom and the group evaluating UM for publication). Alfred requested "an architectural overview (data structures, file formats, etc.) because then we can figure out how to fit it into IWPS." The presentation needs to: (1) introduce UM as a concept, (2) walk through the implementation from the hackathon, (3) show how UM fits into/complements IWPS.

## Objective

Create a presentation-ready explainer package that covers UM architecture at the level OMA3 needs, with IWPS context. This includes a structured talking-points document and concise NotebookLM-compatible briefs for each section.

## Deliverables

- [x] Presentation explainer document at `docs/presentations/2026-03-12-oma3-architectural-overview.md`
- [x] NotebookLM section briefs at `docs/presentations/2026-03-12-oma3-notebooklm-briefs.md`

## Dependencies

- WO-0147 (alignment analysis, can proceed in parallel)

## Acceptance Criteria

1. Presentation document covers 9 sections with key points, visual suggestions, and NotebookLM briefs.
2. IWPS integration section (Section 7) frames UM as complementary cargo to IWPS's transport plumbing.
3. Document uses correct terminology (OMATrust for product/protocol, OMA3 for consortium).
4. Document frames UM as a specification, not an implementation.
5. Document uses "facets" (not "shards") throughout.
6. Hackathon demo section frames PeerMesh as a proof-of-concept, not a product.
