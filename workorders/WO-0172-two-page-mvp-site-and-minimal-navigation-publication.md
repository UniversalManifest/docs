# WO-0172 -- Two-Page MVP Site, Minimal Navigation, and Publication Preparation

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-12
**Completed:** 2026-04-13

## Objective

Publish the smallest coherent public version of `universalmanifest.net`: a low-noise homepage plus the latest draft specification at `/spec/latest/`, with only those two routes in the primary menu.

## Context

The project currently has a broader public site, but that breadth is now the problem.

- Multiple sprint-era surfaces exist with different visual and structural assumptions.
- The root homepage has already been rebalanced away from being the raw specification shell.
- The latest spec has already moved to `/spec/latest/`, which is important because it is the version currently being shared publicly.

The missing step is to deliberately contract the public site before expanding it again.

This phase must:

- keep the homepage calm and easy to understand,
- make the latest spec feel one click away,
- reduce navigation noise,
- preserve deep-route compatibility without making the homepage carry the full site taxonomy.

## Scope

In scope:

1. Reduce the primary public navigation to `Home` and `Latest Spec`.
2. Ensure the homepage clearly and prominently routes visitors to `/spec/latest/`.
3. Keep the latest spec stable at `/spec/latest/` as the publicly shareable standards destination.
4. De-emphasize, hide, or remove non-MVP navigation and homepage clutter that makes the public front door feel overwhelming.
5. Preserve direct access to existing deeper routes without treating them as part of the MVP menu.
6. Prepare the minimal site for publication verification.

Out of scope:

- Reintroducing the broader docs/reference/governance/use-case surface.
- Extracting the full shared component library.
- Unifying tool surfaces such as Sandbox, Harness, Resolver UI, and Workbench.

## Deliverables

- Minimal public homepage + latest-spec menu model.
- Homepage/spec relationship made explicit in navigation and calls to action.
- Reduced-noise homepage content structure suitable for first-time readers.
- Publication-readiness verification notes for the two-page MVP posture.

## Dependencies

- WO-0171 established the homepage/spec split and repaired the spec shell navigation.

## Execution Notes

- The homepage should explain, orient, and direct. It should not try to summarize the whole project.
- The latest spec remains a first-class public artifact, but subordinate to the homepage at `/spec/latest/`.
- Existing deep routes may remain reachable, but they should not dominate the MVP surface.

## Acceptance Criteria

- [x] The primary public navigation contains only `Home` and `Latest Spec`.
- [x] The homepage makes the latest spec visibly reachable in one click.
- [x] The homepage is less noisy and less overwhelming than the current broader public shell.
- [x] `/spec/latest/` remains stable and clearly positioned as the live spec surface.
- [x] Deep links remain accessible even though they are no longer first-class in the MVP menu.
- [x] The site build and publication-prep verification pass with the MVP structure.
