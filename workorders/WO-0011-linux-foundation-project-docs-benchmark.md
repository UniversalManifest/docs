# WO-0011 — Linux Foundation project documentation benchmark (10 projects)

**Status:** NOT_STARTED  
**Created:** 2026-02-12

## Objective

Produce a structured benchmark of Linux Foundation project documentation quality and style using:

- 5 most recently adopted LF projects
- 5 top/flagship LF projects

Total: 10 projects, each with its own report plus synthesis.

## Scope

In scope:

- Identify and validate target 10 projects with source links and dates
- Create one report per project covering:
  - Depth of content
  - Language/voice/writing style
  - Layout style and design patterns
  - Content chunking strategy
  - Sitemap and IA patterns
- Create cross-project synthesis with reusable recommendations for `universalmanifest.net`

Out of scope:

- Full UI implementation of all recommendations
- Legal/licensing analysis beyond public-source citation hygiene

## Deliverables

- Separate report directory:
  - `research/linux-foundation-projects/2026-02/`
- Ten individual reports:
  - `research/linux-foundation-projects/2026-02/project-01-*.md`
  - ...
  - `research/linux-foundation-projects/2026-02/project-10-*.md`
- Master synthesis:
  - `research/linux-foundation-projects/2026-02/SYNTHESIS.md`
- Index:
  - `research/linux-foundation-projects/2026-02/INDEX.md`

## Acceptance criteria

- [ ] Exactly 10 project reports are present (5 recent + 5 top)
- [ ] Each report includes all required dimensions (depth, voice, layout, chunking, sitemap)
- [ ] Sources are listed for each project report
- [ ] Synthesis provides specific actionable standards for `universalmanifest.net`
- [ ] Output directory is self-contained and easy to navigate

## Dependencies

- `docs/workorders/WO-0009-professional-docs-site-universalmanifest-net.md`
- Public Linux Foundation project documentation sites

