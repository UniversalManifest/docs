# Home-Cluster Page Content Architecture and Source Map

**Date:** 2026-04-22  
**Status:** Completion report for `WO-0196`

## Purpose

Define the page-by-page role of the `Home` cluster so the future public experience is built from clear page boundaries instead of one overloaded homepage.

## Home-cluster pages

| Page | Goal | Reader depth | Primary source files | Must include | Must exclude |
| --- | --- | --- | --- | --- | --- |
| `Overview` (`/`) | first-contact explanation and routing | Level 0 | `README.md`, `about/why-um.md`, `about/one-pager.md` | short definition, concrete problem, entry links into `Use Cases`, `Explorer`, `Latest Spec` | long standards comparison, audience taxonomy, deep implementation detail |
| `Use Cases` (`/use-cases/`) | narrative overview of strongest public scenarios | Level 1 | `use-cases/*.md`, `integrations/*.md` | curated scenario families, short summaries, links to deeper lanes | raw architecture explanation, route-matrix clutter |
| `Explorer` (`/explorer/`) | interactive exploration of concrete lanes | Level 1 | content packs, integration docs, public proof links | lane selector, hero asset, exact scenario framing, deeper expandable detail | generic homepage intro copy, giant prose wall |
| `How It Works` (`/how-it-works/`) | conceptual explanation of the UM model | Level 2 | `PROJECT-VISION.md`, `getting-started/universal-manifest-overview.md`, `README.md` | envelope model, pointers, consent, TTL, projection logic | audience segmentation, exhaustive standards comparison |
| `Standards Fit` (`/standards-fit/`) | explain where UM fits among adjacent standards | Level 2 | `about/standards-landscape.md`, `about/standards-positioning.md`, `PROJECT-VISION.md` | what UM is not, what it complements, relationship to adjacent ecosystems | implementation walkthroughs, feature-matrix sprawl on the homepage |

## Source-map rules

### `Overview`

Use:

- the shortest true definition of UM,
- the fragmentation problem,
- one route to the explorer,
- one route to the latest spec.

Do not use:

- internal publication-language,
- repeated reassurance that the spec is easy to find,
- large audience grids.

### `Use Cases`

Use:

- scenario families,
- concise use-case blurbs,
- links to lanes and audience pages.

Do not use:

- detailed standards-comparison prose,
- a second full conceptual primer.

### `Explorer`

Use:

- lane-specific assets,
- lane-specific reasoning,
- proof links,
- content packs that can also feed audience pages.

Do not use:

- homepage-generalized copy,
- architecture diagrams without a lane context.

### `How It Works`

Use:

- envelope/container framing,
- subject / claims / consent / pointers / TTL,
- portable summary versus authoritative source.

Do not use:

- persona narratives as the main structure,
- standards-landscape comparison tables.

### `Standards Fit`

Use:

- relationship to VCs, DIDComm, Solid, OIDC, DIDs, signature profiles, and subject runtimes.

Do not use:

- product-style benefit cards,
- first-contact public persuasion copy.

## Duplicate and conflict review

Existing pages that overlap with the future `Home` cluster:

- `/about/why-um/`
- `/about/one-pager/`
- `/about/standards-landscape/`
- `/use-cases/`
- `/getting-started/universal-manifest-overview/`

These should not all disappear. But they should stop competing with the root page for first-contact explanation.

Recommended future posture:

- `Home` cluster becomes the primary public onboarding family.
- existing `about/*` pages become support/reference surfaces.
- `Use Cases` remains canonical inside the `Home` cluster.

## Implementation implication

UI implementation should treat the `Home` cluster as five pages with different jobs, not as one page with five sections.

That is the main output of this work order.
