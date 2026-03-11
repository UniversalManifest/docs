---
status: COMPLETED
created: 2026-03-11T20:30:00Z
updated: 2026-03-11T20:45:00Z
owner: Standards Alignment
priority: P0 (blocks OMA3 presentation on 2026-03-12)
tags: [iwps, oma3, alignment, portaling, architecture]
---

# WO-0147: IWPS–Universal Manifest Alignment Analysis and Integration Strategy

## Context

OMA3 wants to publish the Universal Manifest standard. Their existing IWPS (Inter-World Portaling Standard) v0.3 defines transport-level portaling (two API calls: Query + Teleport) but has TBD sections for asset transfer, look-and-feel, payments, and portable state. UM fills precisely these gaps. Tomorrow (2026-03-12) there is a presentation to OMA3 where this complementary relationship needs to be clearly articulated.

## Objective

Create a comprehensive alignment document showing how IWPS and UM are complementary (plumbing vs. cargo), mapping IWPS TBD sections to UM capabilities, and identifying integration points.

## Deliverables

- [x] Alignment analysis document in `docs/reports/` — [`2026-03-11-iwps-um-alignment-analysis.md`](../reports/2026-03-11-iwps-um-alignment-analysis.md)

## Dependencies

- WO-0146 (IWPS localization, can proceed in parallel using research summary)

## Acceptance Criteria

1. Alignment document covers executive summary, layer mapping, integration points, mutual value-add, proposed integration architecture, gap analysis, and OMA3 recommendations.
2. Document uses correct terminology (OMATrust for product/protocol, OMA3 for consortium).
3. Document frames UM as a specification, not an implementation.
4. Document uses "facets" (not "shards") throughout.
