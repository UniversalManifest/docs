# WO-0177 -- Staged Tool and Proof Surface Reintegration Under Shared Shell

**Status:** COMPLETED
**Priority:** P1
**Created:** 2026-04-12

## Objective

Reintroduce the interactive tool and proof surfaces after the reading surfaces are aligned, using a coherent shared tool shell instead of the current collection of differently styled wrappers and static pages.

## Context

The project’s tools are important, but they should not return to the front door until the public reading surfaces are unified and the homepage/spec MVP is already stable. When they do return, they need their own shared shell rather than being folded awkwardly into prose-first layouts.

## Scope

In scope:

1. Define a shared shell for Resolver UI, Harness, Workbench, Concept Explorer, and Sandbox-adjacent routes.
2. Reintroduce tool/proof surfaces in deliberate waves after the reading-surface reintegration.
3. Normalize shared navigation, context strips, and route framing for interactive surfaces.
4. Reduce sprint-era visual fragmentation across tool wrappers.

Out of scope:

- Redesigning immutable machine-readable endpoints.
- Changing core normative spec artifacts.
- Reworking tool internals unrelated to shell/layout unification.

## Deliverables

- Shared tool-shell pattern.
- Staged reintegration plan for proof and interactive surfaces.
- Tool-route visual/frame unification across the selected surfaces.

## Progress Notes

- `site/src/layouts/ToolSurfaceLayout.astro` now exists as the first shared shell pattern for tool/proof entry routes.
- `site/src/pages/learning/index.astro` has been rebuilt on that shell as the first calmer hub for sandbox, workbench, harness, proof journeys, and standards/discovery boundary framing.
- `site/src/pages/sandbox/index.astro` now also runs under the shared tool shell. The sandbox chooser no longer owns the whole route as a standalone document.
- `site/src/components/sandbox/ScenarioModal.astro` is now embeddable: the standalone topbar is optional, and the sandbox chooser can be hosted inside the shared tool shell without changing scenario internals.
- `site/src/styles/sandbox/modal.css` no longer relies on global `html, body` assumptions for the chooser route, which keeps the sandbox entry aligned with the broader public shell.
- `site/src/pages/workbench/index.astro` now hosts the manifest workbench inside the shared tool shell instead of dumping standalone HTML at the route root.
- The raw workbench payload moved behind the shared route boundary to `site/public/workbench/app/index.html`, while `site/public/workbench/index.html` now redirects legacy direct-entry traffic to `/workbench/app/`.
- This completion slice deliberately preserves the workbench internals as a stable embedded payload rather than redesigning the client-side editor itself.
- Browser verification completed successfully on `http://127.0.0.1:4325/learning/`, `http://127.0.0.1:4325/sandbox/`, and `http://127.0.0.1:4325/workbench/` after a clean `npm run build`, including iframe/payload verification and fixture loading inside the workbench app.

## Dependencies

- WO-0175 establishes the internal UI foundation.
- WO-0176 restores the reading-surface family first.

## Acceptance Criteria

- [x] Tool and proof surfaces return under a deliberate shared shell.
- [x] Interactive routes no longer feel like unrelated products.
- [x] The public site preserves the calm two-page MVP front door even as richer surfaces return behind it.
