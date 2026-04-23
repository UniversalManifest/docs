# Audience Landing Family Architecture and Route Strategy

**Date:** 2026-04-22  
**Status:** Completion report for `WO-0197`

## Purpose

Define the audience landing-page family as a downstream route family that the `Home` cluster and explorer can link into without turning the homepage into audience-taxonomy clutter.

## Canonical audience route family

- `/audiences/metaverse/`
- `/audiences/eu-ssi/`
- `/audiences/platforms/`
- `/audiences/privacy-and-consent/`
- `/audiences/venues-and-spatial/`
- `/audiences/credential-and-personhood/`

## Audience-page role

Each audience page should answer:

1. Why UM matters to this audience specifically.
2. Which use cases matter most to them.
3. Which adjacent standards, ecosystems, or initiatives matter in their language.
4. Which proof, docs, and spec surfaces they should inspect next.

## Audience-to-source map

| Audience route | Core source material | Main supporting surfaces |
| --- | --- | --- |
| `/audiences/metaverse/` | `integrations/metaverse.md`, `integrations/rp1-spatial-fabric.md` | `use-cases/creator.md`, `proof/journeys`, metaverse-related diagrams/animations |
| `/audiences/eu-ssi/` | `integrations/did-vc.md`, `about/standards-landscape.md`, `about/standards-positioning.md` | `/spec/latest/`, `/conformance/`, DID/VC and identity-related proof surfaces |
| `/audiences/platforms/` | `use-cases/app-developer.md`, `integrations/reference-runtime.md` | `/docs/`, `/sandbox/`, `/workbench/`, `/spec/latest/` |
| `/audiences/privacy-and-consent/` | `use-cases/privacy.md`, `integrations/gpc-global-privacy-control.md`, `integrations/smart-glasses.md` | consent diagrams, `/sandbox/`, `/proof/*` |
| `/audiences/venues-and-spatial/` | `use-cases/venue-operator.md`, `integrations/rp1-spatial-fabric.md`, `integrations/smart-glasses.md` | edge/offline examples, `/sandbox/`, `/resolver/` |
| `/audiences/credential-and-personhood/` | `integrations/proof-of-personhood.md`, `integrations/did-vc.md`, `integrations/education-credentials.md` | `/spec/latest/`, `/conformance/`, journey evidence |

## Relationship to the `Home` cluster

- `Home` cluster = use-case-first, low-noise, progressive depth.
- Audience pages = tailored downstream destinations.

The explorer should link into the corresponding audience page for each lane where appropriate.

The homepage should only expose audience links selectively and secondarily. It should not lead with them.

## Boundary rules

Audience pages should contain:

- ecosystem-specific framing,
- specific adjacent-standard references,
- targeted proof and next-step links.

Audience pages should not contain:

- the entire general explanation of UM,
- repeated first-contact hero copy,
- a giant route index.

## Implementation implication

Audience pages should share the public shell and have consistent structure, but they should be treated as a separate family from the core `Home` tabs.
