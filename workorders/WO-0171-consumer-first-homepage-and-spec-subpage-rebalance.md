# WO-0171 -- Consumer-First Homepage, Spec Subpage Rebalance, and Spec Navigation Repair

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-12

## Objective

Restore `universalmanifest.net` as a consumer-friendly front door by replacing the current spec-first root route with a homepage that explains the problem Universal Manifest solves across many user types, while moving the latest W3C-style specification to a stable subordinate route and repairing the navigation on that specification surface.

## Context

The current live root-route implementation does not match the intended public-adoption posture.

- `site/src/pages/index.astro` currently serves the raw W3C-style specification HTML shell directly.
- `site/src/pages/docs/index.astro` already provides a curated documentation entry point, but it is not the public front door.
- The current homepage therefore behaves like a standards artifact, not a product-facing or adopter-facing landing surface.

That is the wrong outside-in order for this stage of the project.

Universal Manifest needs the homepage to do a different job:

- explain the core problem in plain language
- show why a portable manifest helps many different user types
- route visitors by intent and audience
- make the standards/reference material easy to reach without forcing every visitor through it first

At the same time, the latest W3C-style specification remains important and should stay prominent. It just should not remain the public homepage. Its navigation also needs improvement so standards readers can move cleanly between the spec, the broader site, and the key supporting routes.

## Scope

In scope:

1. Replace the root-route public experience with a consumer-first homepage.
2. Move the latest W3C-style specification to a stable subordinate route.
3. Repair the navigation model on the W3C-style specification page so it is usable as a standards surface inside a broader site, not as an isolated homepage shell.
4. Define audience lanes and message hierarchy for the homepage, including at least:
   - evaluators and decision-makers
   - implementers and architects
   - product/platform teams
   - domain adopters exploring specific use cases
   - agents/tooling/proof explorers
5. Preserve access to the versioned spec routes and existing deep reference links.
6. Clarify how the homepage, `/docs/`, `/spec/`, `/reference/`, `/sandbox/`, `/integrations/`, and `/for-agents/` should relate to one another.

Out of scope:

- Rewriting the full documentation corpus.
- Changing the core normative contract in `spec/`.
- Broad resolver/runtime changes unrelated to the public standards and adoption surfaces.

## Deliverables

- A new consumer-first root homepage implementation.
- A stable subordinate route for the latest W3C-style specification.
- Updated site navigation connecting homepage, docs, spec, integrations, proof, and agent/discovery surfaces.
- Repaired navigation inside the W3C-style specification shell, including clear outbound routing to the rest of the site.
- An implementation report documenting the route change, IA, navigation behavior, and compatibility decisions.

Completed artifacts:

- `site/src/pages/index.astro`
- `site/src/pages/spec/latest.astro`
- `site/src/pages/docs/index.astro`
- `site/src/layouts/PublicSurfaceLayout.astro`
- `docs/W3C-STYLE-SPEC.html`
- `docs/reports/2026-04-12-consumer-homepage-and-spec-subpage-rebalance.md`

## Dependencies

- WO-0157 — Landing surface and multi-layer interaction architecture
- WO-0161 — Landing page and docs secondary route implementation
- WO-0164 — Docs-root relocation and warning-free build baseline
- WO-0165 through WO-0170 — W3C-style specification and architecture/spec hardening wave

## Execution Notes

- The homepage should optimize for comprehension, audience routing, and adoption energy rather than trying to act as a condensed specification.
- The W3C-style specification should remain first-class and easy to find, but as a standards destination rather than the default public landing experience.
- The current spec page navigation fix is part of this work order, not a separate cleanup item.
- Existing versioned spec routes such as `/spec/v01/` and `/spec/v02/` must remain stable.
- If redirects or canonicals are needed, they should reinforce rather than blur the distinction between:
  - public landing
  - curated docs entry
  - normative specification
  - proof/tooling surfaces

## Acceptance Criteria

- [x] `/` is a consumer-first homepage rather than the raw spec shell.
- [x] The latest W3C-style specification is accessible at a stable subordinate route.
- [x] The homepage clearly explains the value of UM across multiple user types and routes visitors by intent.
- [x] The current specification surface has repaired navigation that connects it cleanly to the wider site.
- [x] Existing deep docs/spec/reference routes remain stable or redirect predictably.
- [x] The site build passes with the new route structure and navigation model.
