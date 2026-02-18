# WO-0015 — First-time overview and visual onboarding

**Status:** IN PROGRESS  
**Created:** 2026-02-18

## Objective

Ensure first-time readers can immediately understand:

1. what Universal Manifest is,
2. who it is for,
3. how to start using it,

without prior project context.

This includes a visual-first overview with maintained diagrams.

## Scope

In scope:

- Add a dedicated overview page in docs that explains UM in plain language.
- Add a visual diagram section for high-level architecture and flow.
- Add Excalidraw source-of-truth structure for diagram maintenance.
- Connect overview page to quick start, spec, conformance, and proof pages.

Out of scope:

- Rewriting all deep spec pages for beginner audience
- Product marketing copy beyond technical onboarding

## Deliverables

- Overview page in site docs (`site/src/content/docs/getting-started/`)
- First overview diagram template (published asset)
- Diagram source workspace structure for Excalidraw (`docs/diagrams/`)

## Acceptance criteria

- [x] A first-time overview page exists and is linked from docs navigation paths.
- [x] Page includes a high-level visual diagram.
- [x] Diagram source/edit workflow is documented for maintainers.
- [ ] Reader testing confirms a new implementer can answer: "What is UM?" and "How do I start?" after reading only this page.

## Dependencies

- `docs/site/EDITORIAL-STYLE-GUIDE.md`
- `docs/site/INFORMATION-ARCHITECTURE.md`
- `docs/PROJECT-VISION.md`
