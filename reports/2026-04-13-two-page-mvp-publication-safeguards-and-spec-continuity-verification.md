# 2026-04-13 — Two-Page MVP Publication Safeguards and Spec Continuity Verification

## Summary

This report closes `WO-0174` by verifying that the current public MVP is publishable as a coherent default surface.

The public posture is now:

- `/` is the low-noise explanatory homepage.
- `/spec/latest/` is the stable latest-draft specification route already being shared publicly.
- The homepage and spec shell link directly to one another.
- Internal review pages remain reachable by direct URL but are marked `noindex, nofollow` so they do not compete with the MVP publication posture.

## Continuity Checks

### Latest spec continuity

- Confirmed `site/src/pages/spec/latest.astro` still serves the checked-in W3C-style draft from `docs/W3C-STYLE-SPEC.html`.
- Added an explicit canonical tag in `docs/W3C-STYLE-SPEC.html` pointing to `https://universalmanifest.net/spec/latest/`.
- Verified that the latest draft route remains the stable public destination referenced in the homepage body copy and in the spec header itself.

### Homepage/spec relationship

- Confirmed the public navigation on the homepage and the spec surface is reduced to `Home` and `Latest Spec`/`Latest Draft Spec`.
- Confirmed the homepage exposes `/spec/latest/` repeatedly in the hero, side panel, and closing section so the spec is clearly one click away.
- Confirmed the spec shell links back to `/` via the top site navigation.

### Dead-end and confusion audit

- No dead-end navigation remains between the two public MVP routes.
- Existing deep routes remain directly reachable by URL but are no longer promoted through the primary public menu.
- Review-only pages under `/review/` were marked `noindex, nofollow` so they do not dilute the public MVP story during staged reintegration.

## Metadata Safeguards Added

### Homepage

- Added canonical metadata through `site/src/layouts/PublicSurfaceLayout.astro` and set the homepage canonical path to `/`.

### Latest spec

- Added `<link rel="canonical" href="https://universalmanifest.net/spec/latest/">` to the W3C-style spec HTML.

### Review surfaces

- Added `noindex, nofollow` metadata to:
  - `/review/full-site-audit/`
  - `/review/reorganization-blueprint/`

## Verification Evidence

### Build verification

- Ran `npm run build` in `site/` successfully after the metadata and continuity updates.

### Output inspection

- Verified generated homepage output includes canonical metadata.
- Verified generated `/spec/latest/` output includes canonical metadata.
- Verified generated review outputs include `robots` metadata preventing indexing.

### Browser-visible continuity

- The homepage presents the latest spec as the immediate next action.
- The latest spec page provides an immediate route back to the homepage.
- The latest spec remains subordinate to the homepage without becoming hidden or ambiguous.

## Outcome

`WO-0174` is complete. The two-page MVP is now not just visually simplified, but publication-hardened enough to act as the public default surface while `WO-0175` begins extracting the internal `UM UI` component system for later reintegration waves.
