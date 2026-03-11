# WO-0092 — Create Standalone Third-Party Adoption Guide

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-03-01
**Priority:** P0 (Critical)
**Source:** Project Completeness and Vision Audit (2026-03-01), Gaps 5, 6, 24, Recommended Actions P0-2, P1-10
**Tags:** [docs], [site], [onboarding]
**Blocks:** External adopter onboarding pathway
**Dependencies:** Coordinates with WO-0055 (Adopter Onboarding Document Package)
**Estimated effort:** 4-6 hours

## Objective

Create a standalone "How to Adopt Universal Manifest" guide that consolidates the adoption tier model (from `DEPTH-AND-SCOPE.md` Tier 0-4), the adoption path (from `full-briefing.md` Level 1-5), and the quick start into a single, public-facing document on the site.

## Why this work matters

The completeness audit found that there is no standalone adoption guide for third parties. The adoption tier model and adoption path are excellent but buried in internal docs (`DEPTH-AND-SCOPE.md` and `full-briefing.md`). External adopters have no single document that answers "what level of commitment does adoption require, and what do I get at each tier?"

## Scope

### New files to create

1. **`site/src/content/docs/getting-started/adopt.md`** — Public-facing adoption guide on the site

### Content to consolidate

From `docs/DEPTH-AND-SCOPE.md` (lines 150-161) — Adoption tiers:
- Tier 0: Parse-only (validate `@type`, TTL, treat unknown fields as opaque)
- Tier 1: Pointers consumer (use `pointers` to fetch canonical content)
- Tier 2: Projection renderer (render known `facets`)
- Tier 3: Verified consumer (enforce signature verification + TTL)
- Tier 4: Issuer (produce signed manifests)

From `docs/explainers/full-briefing.md` — Adoption path (Level 1-5)

From `site/src/content/docs/getting-started/quick-start.md` — Practical getting started steps

### Guide structure

1. Who should adopt UM (audience definition)
2. Adoption tiers — what you get at each level of commitment
3. Minimum viable adoption (Tier 0 walkthrough)
4. Progressive adoption path (Tier 0 through Tier 4)
5. Resources for each tier (spec docs, fixtures, conformance suite, reference implementation)
6. FAQ for evaluators and adopters

### Sidebar integration

Add the adoption guide to the "Getting Started" section of the site sidebar.

### Relationship to WO-0055

WO-0055 creates a comprehensive implementation guide (`docs/guides/IMPLEMENTATION-GUIDE.md`) targeted at developers who have decided to implement. This WO creates the higher-level guide that helps decision-makers and architects evaluate WHETHER to adopt and at what level. The two documents complement each other and should cross-link.

## Acceptance criteria

- [ ] Adoption guide exists as a published site page.
- [ ] All five adoption tiers are clearly described with what each requires and provides.
- [ ] A developer or architect can determine their adoption tier within 5 minutes of reading.
- [ ] The guide links to the implementation guide (WO-0055), conformance suite (WO-0053), and Build Your Own Implementation page (WO-0085).
- [ ] `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean` succeeds.

## Validation commands

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build:clean`
- Manual review of adoption guide content completeness.
