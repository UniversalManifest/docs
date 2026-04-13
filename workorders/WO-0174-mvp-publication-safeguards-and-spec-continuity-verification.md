# WO-0174 -- MVP Publication Safeguards and Spec Continuity Verification

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-04-12
**Completed:** 2026-04-13

## Objective

Publish the two-page MVP safely by verifying continuity for the publicly shared latest spec, documenting the homepage/spec relationship, and checking that the contracted public site does not create confusion or dead ends.

## Context

The latest spec is not just another subpage. It is already a publicly shared artifact. The homepage can take over the public front-door role, but the spec move must feel intentional and stable rather than disruptive.

This work order protects that transition.

## Scope

In scope:

1. Verify continuity of `/spec/latest/` as the public latest-spec destination.
2. Audit homepage and spec-shell links so the relationship between the two pages is explicit.
3. Check for dead ends or stale expectations created by the old spec-first homepage posture.
4. Define and verify any redirect, canonical, or compatibility behavior needed for the MVP publication.
5. Record publication verification evidence for the two-page MVP.

Out of scope:

- Broad content reintegration.
- Design-system extraction.
- Tool-shell rework.

## Deliverables

- Publication verification checklist and evidence for the two-page MVP.
- Explicit continuity guidance for the latest spec route.
- Compatibility/redirect notes if any legacy expectations require them.

## Progress Notes

- Confirmed the public MVP transition is coherent: homepage and spec each link directly to the other, and the homepage repeatedly exposes `/spec/latest/` as the public draft route.
- Added canonical metadata for the homepage and the latest draft specification so the metadata layer matches the new route posture.
- Marked the internal `/review/` audit surfaces as `noindex, nofollow` so they do not dilute the MVP publication story while the broader site remains accessible behind the minimal public shell.
- Captured publication verification evidence in `docs/reports/2026-04-13-two-page-mvp-publication-safeguards-and-spec-continuity-verification.md`.

## Dependencies

- WO-0172 establishes the contracted MVP shell.
- WO-0173 tunes the homepage so publication checks evaluate the intended messaging surface.

## Acceptance Criteria

- [x] `/spec/latest/` is verified as the stable public latest-spec destination.
- [x] The homepage clearly explains where the latest spec lives.
- [x] No dead-end public navigation remains from the homepage/spec transition.
- [x] Publication checks confirm the two-page MVP is ready to serve as the public default surface.
