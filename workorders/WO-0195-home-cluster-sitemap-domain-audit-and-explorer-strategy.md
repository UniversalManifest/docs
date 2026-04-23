# WO-0195 -- Home-Cluster Sitemap, Domain Audit, and Explorer Strategy

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-22
**Completed:** 2026-04-22

## Objective

Define the next public homepage architecture as a content-first home cluster rather than a single long landing page, including:

1. a sitemap for the `Home` cluster that keeps the global menu limited to `Home` and `Latest Spec`,
2. a domain-of-thought and depth-of-understanding audit for the existing project corpus,
3. an interactive explorer strategy that leads with the highest-priority use cases, starting with metaverse portaling and avatar/content portability,
4. a downstream audience-landing-page strategy so critical audiences can be addressed directly without turning the homepage into an audience taxonomy.

## Context

The current homepage reset strategy correctly identified the need for lower-noise communication, but it still risked collapsing the public story into a single general-purpose reader. That is not enough for Universal Manifest.

The project now needs a better structure:

- keep the top-level public navigation minimal,
- stop trying to cram the whole adoption story into one homepage,
- organize the `Home` experience around multiple concrete use-case and understanding paths,
- route to audience-specific landing pages as separate destinations rather than homepage clutter,
- let content strategy come before homepage implementation.

The user direction for this work is explicit:

- metaverse/MSF-facing portability should be a lead public lane,
- the homepage should support a second level of `Home`-specific navigation,
- an interactive infographic/explorer pattern should be considered,
- sitemap and IA must come before new website implementation.

## Scope

In scope:

1. Define the home-cluster route architecture and local-tab model.
2. Audit the project into domains of thought and levels of depth.
3. Identify which existing pages/assets should seed the new home-cluster content.
4. Define the interactive explorer concept and content structure.
5. Prioritize use-case lanes for the explorer, with metaverse portaling first.
6. Define the audience-landing-page layer and where it should sit in the IA.
7. Record the content-before-website implementation sequence.

Out of scope:

- implementing the new homepage UI,
- rewriting the final homepage copy,
- migrating existing routes or retiring old ones,
- changing the global public menu away from `Home` and `Latest Spec`.

## Deliverables

- Strategy report:
  - `docs/reports/2026-04-22-home-cluster-sitemap-domain-audit-and-explorer-strategy.md`
- Updated work-order index and status docs reflecting the new planning output.

## Completion Notes

- Defined the recommended `Home` cluster around local sub-navigation rather than a single overloaded root page.
- Defined the domain-of-thought model for public onboarding content.
- Defined the depth-of-understanding model so homepage content stops mixing first-contact explanation with evaluator and implementer material.
- Defined the interactive explorer pattern and its prioritized use-case lanes.
- Defined audience-specific landing pages as a separate route family that the homepage and explorer can direct toward.
- Recorded the content-first sequence: sitemap → content architecture → explorer content packs → UI implementation.

## Dependencies

- WO-0171 through WO-0178 established the current public homepage/spec split and calm MVP posture.
- WO-0179 established the full surface map.
- WO-0180 through WO-0182 established keep/merge/alias/retire posture for the broader site.
- WO-0195 responds directly to the current homepage-message audit and follow-on direction from the user.

## Acceptance Criteria

- [x] A concrete home-cluster sitemap exists.
- [x] The strategy preserves the global `Home` + `Latest Spec` menu model.
- [x] The audit organizes the project into domains of thought and levels of depth.
- [x] The explorer concept is defined as a content model, not just a vague interaction idea.
- [x] Metaverse portaling is explicitly prioritized as the lead explorer lane.
- [x] Audience landing pages are defined as a separate IA layer rather than homepage clutter.
- [x] The implementation order is content-first rather than UI-first.
