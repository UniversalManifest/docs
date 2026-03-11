---
status: COMPLETED
created: 2026-03-11T20:30:00Z
updated: 2026-03-11T20:45:00Z
owner: Documentation & Developer Experience
priority: P1
tags: [video, explainer, notebooklm, hierarchy, discovery, vignettes]
---

# WO-0149: Video Explainer Hierarchy of Discovery and NotebookLM Brief System

## Context

The current vignette approach (WO-0145) produced 5 detailed motion-graphics scripts, but the actual production pipeline uses NotebookLM, which has access to the full UM knowledge vault and only needs short directive briefs (~500 chars) telling it what to focus on and what NOT to cover. The scripts are also flat — there is no guided discovery hierarchy. The user needs a layered system where different audiences find their entry point and drill down. Two standard lengths: short vignette (2 min) and deep explainer (6 min).

## Objective

Design the complete video explainer hierarchy and create the NotebookLM brief system. This replaces the detailed scene-by-scene script approach with focused directives.

## Deliverables

1. [x] Hierarchy of discovery document defining all levels and audience paths — [`docs/scripts/video-hierarchy-of-discovery.md`](/docs/scripts/video-hierarchy-of-discovery.md)
2. [x] NotebookLM brief for each video in the hierarchy (~500 chars each, specifying focus and exclusions) — included in hierarchy document
3. [x] Updated [`docs/scripts/vignette-catalog.md`](/docs/scripts/vignette-catalog.md) reflecting the new structure

## Dependencies

- Existing scripts in `docs/scripts/` serve as source material but need restructuring.
- WO-0145 vignette catalog and Batch 1 scripts (V-01 through V-05) are reference material for the NotebookLM production pipeline, not direct production scripts.
