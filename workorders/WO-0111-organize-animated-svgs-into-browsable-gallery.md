# WO-0111 — Organize Animated SVGs into Browsable Gallery on the Site

**Status:** COMPLETED
**Created:** 2026-03-01
**Priority:** P2 (Nice-to-have)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gap 26, Recommended Action P1-12
**Tags:** [site]
**Blocks:** None (enhancement)
**Dependencies:** WO-0105 (SVG count should be accurate first)
**Estimated effort:** 3-4 hours

## Objective

Organize the 29 production animated SVGs (plus 2 pilot iterations) into a browsable gallery or visual explainer page on the site, presented in a logical teaching sequence.

## Why this work matters

The completeness audit found that production animated SVGs are live but scattered across content pages with no organized gallery or tutorial sequence. The verification agent confirmed 33 total SVGs exist: 29 production, 2 pilots, and 2 test files. An "Animation Gallery" or "Visual Explainer" page would serve as a powerful teaching tool and demonstrate the project's visual communication capability.

## Scope

### New site page

**`site/src/content/docs/about/visual-explainers.md`** (or `about/animation-gallery.md`)

### Content structure

1. **Introduction** — What the animated explainers are and how they were produced
2. **Core concepts** — SVGs explaining the UM data model, lifecycle, and architecture
3. **Integration lanes** — SVGs for each integration domain
4. **Tools and verification** — SVGs for the workbench, harness, and validation flow
5. **Teaching sequence** — Recommended viewing order for newcomers

### Source inventory

- 14 production `scenario-*` prefixed SVGs in `site/public/animations/` (excludes 2 test files)
- 15 numbered SVGs (e.g., `1.3-overlay-lanes.svg`, `5.2-consent-policy-flow.svg`)
- 2 pilot SVGs (`um-*-pilot.svg`) — may be included as historical/comparison items
- 15 static diagrams in `site/public/diagrams/`

### Sidebar integration

Add to the "About" section of the site sidebar.

## Acceptance criteria

- [x] Gallery page exists on the public site.
- [x] All production animated SVGs are included with titles and brief descriptions.
- [x] SVGs are organized in a logical teaching sequence.
- [x] Each SVG is viewable directly on the page (embedded, not just linked).
- [x] `cd site && npm run build:clean` succeeds.

## Validation commands

- `cd site && npm run build:clean`
- Manual review of gallery page in browser.
