---
status: COMPLETED
created: 2026-03-11T13:54:00Z
updated: 2026-04-02T02:19:52Z
owner: Documentation & Developer Experience
priority: HIGH
tags: [video, explainer, youtube, ui-vignettes]
---

# WO-0145: Vignette Video Library & Explainer Project Tracking

## Context
The universalmanifest site currently has no video embeds or video placeholder buttons. The existing "play" buttons in the sandbox are step-through animation controls for interactive scenarios, not video playback elements. Vignette explainers are a net-new addition to the site. Simultaneously, there is a need for highly specific, modular explainer videos that break down Universal Manifest concepts independently of PeerMesh.

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
- [x] Comprehensive markdown catalog of needed vignettes — [`docs/scripts/vignette-catalog.md`](/docs/scripts/vignette-catalog.md)
- [x] Approved scripts for the first batch of 5 priority vignettes (V-01 through V-05)
- [x] Production workflow established for video creation (documented in catalog)
- [x] Strategy handoff to the active hierarchy pipeline completed (`WO-0149` + `docs/scripts/video-hierarchy-of-discovery.md` + `docs/scripts/production-queue.md`).

## UI Audit Results (2026-03-11)

The site audit found:
- **Zero** existing video embeds, YouTube URLs, or video placeholder links.
- **Sandbox play buttons** (in `StepController.astro` and `[...scenario].astro`) control step-through animation engines, not video playback.
- Vignette video embeds are a **net-new UI feature** to be introduced.

### Planned UI Placement
1. Sandbox scenario category headers — "Watch the explainer" links
2. Key concept pages (Overview, Spec, Integrations, Adoption Guide) — embedded at top
3. Landing page — featured hero vignette
4. YouTube playlist — all vignettes published sequentially

## Scripted Vignettes (Batch 1 — Core Concepts)

| ID | Title | Script | Status |
|----|-------|--------|--------|
| V-01 | The Portable Envelope | [`vignette-01-portable-envelope.md`](/docs/scripts/vignette-01-portable-envelope.md) | SCRIPTED |
| V-02 | Facets and Pointers | [`vignette-02-facets-and-pointers.md`](/docs/scripts/vignette-02-facets-and-pointers.md) | SCRIPTED |
| V-03 | Default-Deny Consent | [`vignette-03-default-deny-consent.md`](/docs/scripts/vignette-03-default-deny-consent.md) | SCRIPTED |
| V-04 | Cross-World Identity | [`vignette-04-cross-world-identity.md`](/docs/scripts/vignette-04-cross-world-identity.md) | SCRIPTED |
| V-05 | Manifest Resolution | [`vignette-05-manifest-resolution.md`](/docs/scripts/vignette-05-manifest-resolution.md) | SCRIPTED |

## Spatial Fabric Learnings Applied

Key insights from the peer-mesh-spatial-fabric hackathon were incorporated into vignette scripts:
- **Pointer-first architecture** validated: manifests stay under 3 KB by storing URLs, not assets (V-02).
- **Dual-format normalization** proven: portal server accepted both UM v0.1 and Manifest Commons formats (V-01).
- **Cross-renderer identity traversal** demonstrated: same manifest served Portal (Three.js), RP1, and ActivityPub endpoints (V-04).
- **Facet-based privacy** worked in practice: consent toggles enforced at runtime by consuming systems (V-03).
- **Resolver lookup pattern** validated: fetch by UMID, validate client-side (V-05).

## Dependencies
- UI component inventory (completed — audit found no existing video elements).
- Finalization of `script-architectural-overview.md` for executive presentations (completed).

## Remaining Work
- None in `WO-0145` scope after supersession by `WO-0149`.
- Active production/publishing execution is tracked in `docs/scripts/production-queue.md` and follow-on work orders.
