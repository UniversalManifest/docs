# WO-0205 -- Home-Cluster Migration, Harmonization, and Publication Readiness

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-22
**Completed:** 2026-04-22

## Objective

Converge the new `Home` cluster, explorer, and audience landing pages into a publication-ready public experience with harmonized routes, reduced duplication, and verified browser behavior.

## Context

Once the new IA is implemented, the project still needs a bounded convergence step so the new surfaces do not simply add another layer of duplication on top of the current site.

## Scope

In scope:

1. Browser verification of the new `Home` cluster and audience pages.
2. Route harmonization and duplication review against existing public pages.
3. Publication safeguards and continuity checks.
4. Final pass on messaging consistency, shell behavior, and spec discoverability.

Out of scope:

- reopening unrelated site-architecture waves
- changing normative spec artifacts

## Deliverables

- Publication-readiness report for the new home-cluster rollout.
- Route harmonization notes and any necessary cleanup decisions.

## Completion Notes

- Verified the new `Home`-cluster rollout against the built local site using served-route checks and rendered screenshot checks on key pages.
- Confirmed that the global nav remains calm, `/spec/latest/` remains obvious, and the new cluster did not widen the public top-level menu.
- Recorded the convergence and harmonization pass in `docs/reports/2026-04-22-home-cluster-publication-readiness-and-harmonization.md`.

## Dependencies

- WO-0202
- WO-0203
- WO-0204

## Acceptance Criteria

- [x] The new home-cluster rollout passes browser verification.
- [x] Duplication against older public surfaces is identified and handled.
- [x] The global nav remains calm and the spec remains obvious.
- [x] The rollout is coherent enough for publication.
