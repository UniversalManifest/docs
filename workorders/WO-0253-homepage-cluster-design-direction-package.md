# WO-0253: Homepage Cluster Design Direction Package

**Status:** COMPLETED 2026-05-02
**Priority:** P0 (blocks homepage-cluster implementation and reader validation)
**Depends on:** v0.2 publication wave complete; WO-0252 superseded as final design direction
**Unblocks:** WO-0254
**Derived from:** 2026-05-02 objective realignment; user rejection of the current homepage as visually and narratively unacceptable

## Problem

The public entry experience still lacks an approved design concept for the five-page homepage cluster: homepage/overview, use cases, explorer, how it works, and standards fit.

The prior implementation pass (`WO-0252`) improved structure but still failed the user's quality bar. Continuing to patch the homepage code without a design target risks local-optimization drift: technically valid page revisions that still do not make Universal Manifest legible, compelling, or reviewable by first-time readers.

## Objective

Produce a design report, not implementation code, that defines the new public entry experience for the homepage cluster.

The report must make Universal Manifest immediately understandable as a portable, signed context envelope that carries identity, claims, permissions, pointers, proof, and validity rules across systems that do not share one backend.

## Files to read first

- `/Users/grig/work/repo/universalmanifest/.dev/ai/designs/2026-05-01-homepage-cluster-redesign-agent-brief.md`
- `/Users/grig/work/repo/universalmanifest/docs/PROJECT-VISION.md`
- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-SITEMAP.md`
- `/Users/grig/work/repo/universalmanifest/docs/HOME-CLUSTER-COPY-BRIEFS.md`
- `/Users/grig/work/repo/universalmanifest/.dev/ai/orchestration/2026-05-02T03-56-15Z-objective-realignment.md`

## Work to perform

1. Use the self-contained design-agent brief as the primary input. Do not require localhost, repo access, private screenshots, or private files.
2. Diagnose the current homepage cluster across information hierarchy, visual hierarchy, first-screen clarity, copy density, navigation, emotional credibility, and first-reader reaction.
3. Define a new design concept with a concrete visual and narrative model.
4. Define the homepage section sequence with purpose, headline direction, copy length target, visual treatment, and CTA hierarchy.
5. Provide exact recommended hero copy and above-the-fold requirements for desktop and mobile.
6. Define the distinct job of each page:
   - Homepage / Overview
   - Use Cases
   - Explorer / Scenario Explorer
   - How It Works
   - Standards Fit
7. Define the copy architecture, visual direction, interaction model, implementation guidance, and validation checklist.
8. Return a single markdown design report suitable for implementation handoff.

## Files to modify / create

- Create `/Users/grig/work/repo/universalmanifest/.dev/ai/designs/{date}-homepage-cluster-design-report.md`
- Update `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md` only when the design report is delivered.

## Constraints

- Do not write implementation code.
- Do not polish the current page as-is; start over conceptually.
- Do not widen the global navigation beyond `Home` and `Latest Spec`.
- Do not create a generic marketing landing page.
- Do not hide the published v0.2 status or the spec path.
- Do not use localhost, local screenshots, or private repo paths as required inputs for the remote design agent.
- Do not overclaim deferred v0.3+ standards scope.

## Acceptance criteria

- The design report is self-contained enough for an implementation agent to act on.
- The first hero answers "what is Universal Manifest?" without requiring scroll.
- The report defines a distinct job for all five homepage-cluster pages.
- The report avoids wall-of-paragraphs, card dumps, internal project-management language, and vague interoperability claims.
- The report includes exact hero copy, visual direction, section sequencing, page-by-page IA, and implementation guidance.
- The report includes a validation checklist for desktop, mobile, and first-time-reader comprehension.

## Output

Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0253-result.md`
Blocked report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/{date}-wo-0253-BLOCKED.md`

## Closeout Evidence

- Design report: `/Users/grig/work/repo/universalmanifest/.dev/ai/designs/2026-05-02-homepage-cluster-design-report.md`
- Result report: `/Users/grig/work/repo/universalmanifest/.dev/ai/subtask-comms/2026-05-02-wo-0253-result.md`
- Work order index updated: `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-INDEX.md`
- Follow-on implementation work unblocked: `WO-0254` marked `NOT_STARTED` / unblocked on 2026-05-02.
