# WO-0096 — Create "Why UM?" Non-Technical Landing Page for the Site

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P1 (Important)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gaps 2, 28, Recommended Action P0-4
**Tags:** [site], [docs]
**Blocks:** Non-technical audience accessibility
**Dependencies:** WO-0091 (explainers should be on the site first)
**Estimated effort:** 3-4 hours

## Objective

Create a "Why Universal Manifest?" page on the public site that serves as the non-technical entry point for evaluators and decision-makers. This page should lead with the fragmentation problem and human impact, not the JSON-LD format.

## Why this work matters

The completeness audit found that the site overview page leads with a format description ("a portable document format") rather than the human problem ("your data is trapped in silos"). There is no page designed for non-technical evaluators — people who need to understand WHY UM matters before diving into HOW it works.

## Scope

### New file to create

**`site/src/content/docs/about/why-um.md`** (or equivalent path)

### Content structure

1. **The problem** — Lead with the fragmentation problem using concrete, relatable examples. Use the "Swiss Army Knife for personal data" metaphor from the one-pager.
2. **Who is affected** — End users, developers, enterprises, platforms
3. **The solution** — What UM provides (one-paragraph, non-technical)
4. **What makes UM different** — Brief comparison to existing approaches (from competitive positioning in full-briefing)
5. **How to get started** — Links to technical docs for those ready to dive deeper
6. **Real-world scenarios** — 3-4 scenarios adapted from the one-pager or commercial journeys

### Sidebar integration

Link from the "About" section and from the site landing page "Choose a starting path" options (add an "Evaluators" path).

## Acceptance criteria

- [ ] "Why UM?" page exists on the public site.
- [ ] The page leads with the human problem, not the technical format.
- [ ] No JSON-LD, Ed25519, or implementation details appear in the first screen of content.
- [ ] At least 3 real-world scenarios are included.
- [ ] The page is linked from the site landing page.
- [ ] `cd site && npm run build:clean` succeeds.

## Validation commands

- `cd site && npm run build:clean`
- Manual review of page content for non-technical accessibility.
