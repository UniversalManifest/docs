# WO-0177 -- Staged Tool and Proof Surface Reintegration Under Shared Shell

**Status:** PLANNED
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

## Dependencies

- WO-0175 establishes the internal UI foundation.
- WO-0176 restores the reading-surface family first.

## Acceptance Criteria

- [ ] Tool and proof surfaces return under a deliberate shared shell.
- [ ] Interactive routes no longer feel like unrelated products.
- [ ] The public site preserves the calm two-page MVP front door even as richer surfaces return behind it.
