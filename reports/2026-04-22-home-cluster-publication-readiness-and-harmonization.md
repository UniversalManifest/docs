# 2026-04-22 — Home-Cluster Publication Readiness and Harmonization

## Summary

This report records the convergence pass for the `Home`-cluster rollout after implementation.

The goal of this step was not to reopen broad site-architecture work. It was to confirm that the new public cluster behaves coherently, preserves spec discoverability, and does not turn the site into a second round of sprint-era fragmentation.

## Harmonization decisions

### 1. The global nav remains calm

The primary public menu remains:

- `Home`
- `Latest Spec`

The new learning surfaces live inside the `Home` cluster via local tabs rather than widening the primary menu.

### 2. The root page is now only one page in a larger cluster

The root route now behaves as `Overview`, with the rest of the explanatory material distributed across:

- `/use-cases/`
- `/explorer/`
- `/how-it-works/`
- `/standards-fit/`

This prevents the homepage from becoming an all-purpose explanation, audience taxonomy, and standards comparison page at the same time.

### 3. Audience pages are secondary, not first-class top-nav destinations

The audience family exists under:

- `/audiences/*`

These pages are linked from the homepage and explorer but do not widen the top-level nav and do not replace the use-case-first onboarding model.

### 4. Existing secondary reading pages are preserved, not promoted

Legacy-but-still-useful explanatory pages such as:

- `/about/why-um/`
- `/about/one-pager/`

remain available as secondary reading surfaces. This wave did not retire them, but it also did not promote them into the new primary `Home` cluster.

### 5. Spec continuity is preserved

`/spec/latest/` remains the obvious contract path and retains the calm site shell. The new home-cluster rollout does not alter the subordinate spec-route strategy established earlier.

## Verification

Publication-readiness verification included:

- successful `npm run build` in `site/`
- live local served-route checks returning `200` for the key `Home`-cluster, audience, and spec routes
- rendered screenshot verification of:
  - `/`
  - `/explorer/`
  - `/audiences/metaverse/`
- HTML/content verification on:
  - `/how-it-works/`
  - `/standards-fit/`
  - `/use-cases/`
  - `/audiences/eu-ssi/`
  - `/spec/latest/`

## Result

The `Home`-cluster rollout is coherent enough for publication.

What changed:

- the site now has a clear public learning cluster without widening the primary nav,
- the root page is calmer because more of the explanatory burden moved into subordinate cluster routes,
- metaverse and EU SSI now have dedicated audience entry points,
- the latest spec remains obvious and subordinate route continuity is preserved.

What this convergence step intentionally did not do:

- retire older secondary reading pages,
- reopen the wider route-retirement program,
- change the normative spec artifacts.

That boundary keeps this wave aligned with its actual purpose: a publication-ready `Home`-cluster rollout rather than another full-site rearchitecture.
