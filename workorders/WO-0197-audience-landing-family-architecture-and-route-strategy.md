# WO-0197 -- Audience Landing Family Architecture and Route Strategy

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-22
**Completed:** 2026-04-22

## Objective

Define the audience-specific landing-page family that sits one layer below the homepage so Universal Manifest can address critical audiences directly without turning the homepage into an audience taxonomy dump.

## Context

The homepage should remain use-case-first and low-noise. But the project also needs dedicated audience landing pages for strategic pathways such as:

- metaverse and digital worlds
- EU self-sovereign identity / digital identity
- platforms and app teams
- privacy and consent surfaces
- venues and spatial/edge deployments
- credential and personhood ecosystems

These pages need their own route model, purpose, and source map before content writing or implementation starts.

## Scope

In scope:

1. Define the canonical audience landing-page route family.
2. Define the intended role of each audience landing page.
3. Map existing source material into each audience page.
4. Define how homepage/explorer pages should link into these audience destinations.
5. Define what audience pages should contain that the homepage should not.

Out of scope:

- writing final audience-page copy
- implementing the pages
- changing the top-level global nav

## Deliverables

- Audience landing-page route strategy.
- Audience-to-source-content mapping.
- Guidance for how the audience family relates to the `Home` cluster.

## Completion Notes

- Defined the canonical `/audiences/<slug>/` route family and its relationship to the `Home` cluster.
- Defined metaverse, EU SSI, platforms, privacy/consent, venues/spatial, and credential/personhood as the first audience family.
- Recorded the route model, source mapping, and role boundaries in `docs/reports/2026-04-22-audience-landing-family-architecture-and-route-strategy.md`.

## Dependencies

- WO-0195
- WO-0196

## Acceptance Criteria

- [x] Audience landing pages are defined as a distinct route family.
- [x] Each audience page has a documented role and boundary.
- [x] Strategic audiences include metaverse and EU self-sovereign identity.
- [x] The relationship between the `Home` cluster and audience pages is explicit.
