---
status: OPEN
created: 2026-03-11T13:54:00Z
owner: Documentation & Developer Experience
priority: HIGH
tags: [video, explainer, youtube, ui-vignettes]
---

# WO-0145: Vignette Video Library & Explainer Project Tracking

## Context
Various UI pages and components across the project currently feature "play" buttons intended for contextual vignettes. Currently, these buttons link to placeholder or unrelated videos. Simultaneously, there is a need for highly specific, modular explainer videos that break down Universal Manifest concepts independently of PeerMesh. 

## Objective
Establish a tracked project to produce, organize, and publish a comprehensive library of vignette explainers. These short videos must clearly articulate Universal Manifest features as a standalone standard.

## Scope of Work

1. **Audit Existing Placeholders:**
   - Identify all UI locations across the universalmanifest site and related sandboxes that have a video "play" button.
   - Catalog the specific contextual topic each button should address.

2. **Scripting and Storyboarding:**
   - Write highly specific vignette scripts for each cataloged topic.
   - **Crucial Requirement:** Ensure all scripts maintain strict independence from PeerMesh or extraneous implementations. Focus purely on Universal Manifest standard, data structures, and use cases.
   - Utilize existing outlines (e.g., `script-why-it-matters.md`, `script-architectural-overview.md`) as structural baselines.

3. **Production Pipeline Tracking:**
   - Track the production of each video (Voiceover, Animation/Screen Capture, Editing).
   - Establish a standard format and length (e.g., 30-90 seconds).

4. **YouTube/Hosting Deployment:**
   - Create a dedicated Universal Manifest YouTube channel or playlist.
   - Upload completed vignettes with proper SEO, descriptions, and timestamps.
   - Update front-end code to replace placeholder links with the final YouTube URLs.

## Deliverables
- [ ] Comprehensive spreadsheet or markdown catalog of needed vignettes.
- [ ] Approved scripts for the first batch of 5 priority vignettes.
- [ ] Production workflow established for video creation.
- [ ] Final video assets uploaded and linked in the UI.

## Dependencies
- UI component inventory.
- Finalization of `script-architectural-overview.md` for executive presentations (completed).
