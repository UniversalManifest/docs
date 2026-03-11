---
status: COMPLETED
created: 2026-03-11T20:30:00Z
updated: 2026-03-11T20:30:00Z
owner: Standards Alignment
priority: P0
tags: [iwps, oma3, standards, portaling, localization]
---

# WO-0146: IWPS Base Specification v0.3 Localization and Reference Integration

## Context

OMA3 is considering publishing the Universal Manifest standard. Their portaling standard (IWPS) needs to be localized into the UM project as a reference document. Tomorrow (2026-03-12) there is a presentation to OMA3 where architectural alignment between IWPS and UM will be discussed.

## Objective

Convert the IWPS Base Specification v0.3 PDF from https://github.com/oma3dao/iwps-specification/ into a reusable markdown file saved in the UM project's research directory, making it available as a local reference for alignment work.

## Deliverables

1. Markdown version of the IWPS Base Specification v0.3 saved at `docs/research/iwps-base-specification-v0.3.md`
2. README context from the OMA3 repo captured in the file frontmatter and preamble
3. OpenAPI data-url YAML content included as an appendix

## Dependencies

None.

## Acceptance Criteria

- [x] IWPS Base Specification v0.3 faithfully converted to markdown and saved in `docs/research/`
- [x] All normative sections (Section 5) preserved with complete API parameter tables
- [x] All informative examples (Section 6) included
- [x] Frontmatter includes source attribution, version, and localization date
- [x] OpenAPI content appended as reference material

## Completion Summary

This work order is complete.

Delivered:
- Full IWPS Base Specification v0.3 localized to `docs/research/iwps-base-specification-v0.3.md`
- Source content fetched from the OMA3 GitHub repository markdown version (`IWPS Base Specification.md`)
- All 6 top-level sections preserved: Introduction, References, Definitions, Actors/Overview, Specification (Normative), Examples (Informative)
- Complete API parameter tables for Query API (Tables 1-2) and Teleport API (Tables 3-4)
- All 4 identity framework models documented
- All 3 authentication tiers documented
- All 4 teleport communication options documented (Device, Cloud, Hybrid, User Agent)
- All 4 example teleport scenarios included (6.2.1-6.2.4)
- User Agent login flow (6.4.1) included
- Appendix A: OMA3 repository README context and participation terms
- Appendix B: OpenAPI Data URL Metadata API v0.1 YAML (from `openapi/openapi-data-url.yaml`)
- Frontmatter with source URLs, version, localization date, and work order reference
