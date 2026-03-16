# WO-0157 -- Landing Surface and Multi-Layer Interaction Architecture

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-03-15

## Objective

Define the target public-surface architecture for Universal Manifest as a multi-layer system rather than a docs-only site: a primary landing surface, secondary documentation/reference surfaces, agent-friendly discovery surfaces, browser-based tools, and runtime interaction layers across `universalmanifest.net` and `myum.net`.

## Context

The current public experience is still primarily documentation-led. That is useful, but it is no longer the full product need. Universal Manifest needs a coherent outside-in architecture that supports:

- a strong landing page for humans evaluating the standard
- a clear secondary documentation/reference surface
- machine-readable discovery and interaction paths for agents
- browser-based tool surfaces for exploration, validation, and proof
- a clean boundary between standards-host behavior and runtime/resolver behavior

This work order is the program anchor for the follow-on agent-friendly and adoption work. It should establish where each interaction layer belongs and how the site should evolve without collapsing the standards boundary.

## Scope

In scope:

1. Audit the current outside-in surface area across `universalmanifest.net` and `myum.net`.
2. Define the target IA split between:
   - landing/overview
   - docs/reference
   - tools/sandbox/harness/workbench
   - machine-readable discovery
   - runtime/resolver interaction
   - future authenticated or higher-agency interaction layers, if any
3. Define which capabilities belong on:
   - `universalmanifest.net`
   - `myum.net`
   - a future dedicated service or subdomain, if needed
4. Produce a phased implementation sequence for this program.
5. Identify the minimum public artifacts required to demonstrate that better agent ergonomics should improve adoption.

Out of scope:

- Fully implementing the new landing page.
- Implementing every discovery artifact or runtime surface in this work order.
- Turning `universalmanifest.net` into a full agent runtime.

## Deliverables

- Architecture decision package for the public-surface split.
- Surface inventory and target-state interaction map.
- Recommended execution order for downstream implementation work.
- Boundary statement clarifying standards host vs resolver/runtime responsibilities.

Completed artifact:

- `docs/reports/2026-03-15-multi-surface-agent-friendly-architecture.md`

## Dependencies

- None. This work order should execute first and guide WO-0158 through WO-0160.

## Recommended Execution Order

1. WO-0157 -- define the target architecture and sequencing authority.
2. WO-0158 -- publish the machine-readable discovery and interaction entry points.
3. WO-0161 -- implement the landing-first public experience and docs-secondary route split.
4. WO-0159 -- document the agent-facing workflows and public onboarding path.
5. WO-0160 -- formalize completeness, anti-fabrication, and verification gates before broad publication and promotion.

## Acceptance Criteria

- [x] A written target-state architecture exists for landing, docs, tools, discovery, and runtime layers.
- [x] The document explicitly assigns capabilities to `universalmanifest.net`, `myum.net`, or a future separate surface.
- [x] The sequence for WO-0158 through WO-0160 is explicit and justified.
- [x] The architecture preserves the spec-first posture while allowing broader public interaction surfaces.
