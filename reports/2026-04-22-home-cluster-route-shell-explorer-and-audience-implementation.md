# 2026-04-22 — Home-Cluster Route Shell, Explorer, and Audience Implementation

## Summary

This report records the implementation tranche for the new `Home` cluster after the IA and content-model work was completed.

The public site now has a real `Home`-cluster route family instead of forcing the root page to carry every onboarding and adoption concept by itself. The top-level public navigation remains limited to `Home` and `Latest Spec`, while the `Home` cluster now carries a local second-level navigation for the new public learning surfaces.

## Implemented surfaces

The following public routes were implemented or reworked in this tranche:

- `/` — `Overview` page for the `Home` cluster
- `/use-cases/` — moved under the `Home` cluster local-tab model
- `/explorer/` — interactive use-case explorer with lane-driven content updates
- `/how-it-works/` — conceptual model page
- `/standards-fit/` — standards-boundary page
- `/audiences/metaverse/`
- `/audiences/eu-ssi/`
- `/audiences/platforms/`
- `/audiences/privacy-and-consent/`
- `/audiences/venues-and-spatial/`
- `/audiences/credential-and-personhood/`

## Implementation notes

### Shared shell and tabs

The shared public layout now supports an optional `Home`-cluster tab bar below the global header:

- `site/src/layouts/PublicSurfaceLayout.astro`
- `site/src/components/ui/HomeClusterTabs.astro`

This preserves the calm global nav while making the `Home` cluster a real route family.

### Shared content model

The public rollout is powered by one canonical content model in:

- `site/src/data/home-cluster.ts`

That file now holds:

- local-tab definitions
- overview use-case cards
- explorer lane payloads
- audience page payloads
- slug-to-content lookup maps

### Root page reset

The root route was rewritten to behave as the `Overview` tab of the `Home` cluster:

- `site/src/pages/index.astro`

The page now:

- defines Universal Manifest in plain language,
- routes readers into use cases, the explorer, standards fit, and audience pages,
- keeps the latest spec visible without leaking internal publication-strategy language into the body copy.

### Explorer implementation

The explorer route is implemented at:

- `site/src/pages/explorer/index.astro`

It uses a fixed left-rail lane list and a single main content surface that updates in place. The first rendered lane is metaverse portaling, and the page is structured for future lane expansion without changing the shell model.

### Audience landing pages

The audience family is implemented at:

- `site/src/pages/audiences/[audience].astro`

Metaverse and EU SSI are implemented as first-class public audience pages, and the remaining first-wave audience pages use the same structure and shared shell.

## Verification

Implementation verification for this tranche included:

- `npm run build` in `site/` with successful route generation for the new `Home`-cluster and audience pages
- local served-route verification on:
  - `/`
  - `/use-cases/`
  - `/explorer/`
  - `/how-it-works/`
  - `/standards-fit/`
  - `/audiences/metaverse/`
  - `/audiences/eu-ssi/`
  - `/spec/latest/`
- rendered screenshot checks for the homepage, explorer, and metaverse audience page against the local built site

## Outcome

The `Home`-cluster rollout is now implemented as a real public route family rather than a content plan waiting on future UI work. The site can now onboard readers through:

1. an overview page,
2. a use-case list,
3. an interactive explorer,
4. concept and standards-fit pages,
5. audience-specific landing pages,

while preserving the intentionally minimal top-level public navigation.
