# Vignette Video Library — Catalog

**Status:** SUPERSEDED by Hierarchy of Discovery
**Work Order:** [WO-0145](../workorders/WO-0145-vignette-video-library.md) (original) | [WO-0149](../workorders/WO-0149-video-explainer-hierarchy-of-discovery.md) (current)
**Last Updated:** 2026-03-11

> **Important:** The video content strategy has been restructured under WO-0149 into a **Hierarchy of Discovery** system with NotebookLM-driven production. The detailed scene-by-scene scripts (V-01 through V-05) and long-form scripts below are now **reference material** for the NotebookLM production pipeline, not direct production scripts. See [video-hierarchy-of-discovery.md](video-hierarchy-of-discovery.md) for the active video plan, NotebookLM briefs, and the complete hierarchy.

## What Changed

The original approach produced 5 detailed motion-graphics scripts and planned 20 short vignettes (30-60 seconds each). The production pipeline now uses **NotebookLM**, which has access to the full UM knowledge vault and only needs short directive briefs (~500 chars) telling it what to focus on and what NOT to cover.

Key changes:
- **Flat catalog replaced by layered hierarchy:** Videos are organized into 5 levels (Meta/Index, Master Explainer, Audience Summaries, Topic Deep Dives, Micro-Vignettes) so different audiences find their entry point and drill down.
- **Two standard lengths:** 2 min (vignette) and 6 min (deep explainer), replacing the original 30-60 second format.
- **NotebookLM briefs replace scene-by-scene scripts:** Each video has a ~500 char directive specifying focus and exclusions, not a multi-page storyboard.
- **Active video plan:** [video-hierarchy-of-discovery.md](video-hierarchy-of-discovery.md)

## Design Principles (Unchanged)

- **UM-pure:** Every video explains Universal Manifest as a standalone specification. No PeerMesh, no implementation-specific branding.
- **Standalone:** Each video is self-contained within its level. A viewer can watch any single video and learn.
- **Fixture-grounded:** Visual examples reference real UM data structures, fixture patterns, and conformance behaviors.
- **Consistent visual language:** Dark background (#0f172a), warm gold manifest glow, accent colors per facet type. Same character roster as long-form scripts (Alex, Riley, Sam, Jordan, Nova).

## UI Placement Plan (Updated)

Videos are placed according to their hierarchy level:
1. **Landing page** — Level 0 meta/index video (L0-01) as the site entry point and YouTube channel trailer.
2. **Overview / About page** — Level 1 master explainer (L1-01) for the complete picture.
3. **Audience landing pages** — Level 2 audience-specific summaries (L2-01 through L2-05).
4. **Documentation concept pages** — Level 3 topic deep dives (L3-01 through L3-09) embedded alongside relevant docs.
5. **Sandbox scenario pages** — Level 4 micro-vignettes (L4-SB-*) as "Watch the explainer" links.
6. **Integration lane pages** — Level 4 micro-vignettes (L4-IL-*) alongside each integration lane.
7. **Tool documentation** — Level 4 micro-vignettes (L4-TL-*) alongside tool pages.
8. **YouTube** — Full playlist organized by hierarchy level with chapter markers.

---

## Reference Material: Batch 1 Scripts (V-01 through V-05)

These 5 detailed scene-by-scene scripts were produced under WO-0145. They serve as **reference material** for visual production direction, technical accuracy, and NotebookLM knowledge vault context. They are not the direct production input for the NotebookLM pipeline.

| ID | Title | Script | Maps To (Hierarchy) | Role |
|----|-------|--------|---------------------|------|
| V-01 | The Portable Envelope | [vignette-01-portable-envelope.md](vignette-01-portable-envelope.md) | L3-01 | Visual reference, technical detail |
| V-02 | Facets and Pointers | [vignette-02-facets-and-pointers.md](vignette-02-facets-and-pointers.md) | L3-02 | Visual reference, technical detail |
| V-03 | Default-Deny Consent | [vignette-03-default-deny-consent.md](vignette-03-default-deny-consent.md) | L3-03 | Visual reference, technical detail |
| V-04 | Cross-World Identity | [vignette-04-cross-world-identity.md](vignette-04-cross-world-identity.md) | L3-04 | Visual reference, technical detail |
| V-05 | Manifest Resolution | [vignette-05-manifest-resolution.md](vignette-05-manifest-resolution.md) | L3-05 | Visual reference, technical detail |

## Reference Material: Long-Form Scripts

These scripts were written before the hierarchy system and serve as **source material** for the NotebookLM knowledge vault and visual production planning.

| Script | Duration | Maps To (Hierarchy) | Role |
|--------|----------|---------------------|------|
| [script-what-is-um.md](script-what-is-um.md) | 60–90s | L1-01, L3-01, L3-02 | Narrative reference for master explainer and envelope/facets deep dives |
| [script-why-it-matters.md](script-why-it-matters.md) | 60–90s | L2-01, L3-08, L4-IL-* | Scenario reference for executive summary and integration lane overview |
| [script-how-it-works.md](script-how-it-works.md) | 90–120s | L2-02, L3-01, L3-02, L3-03, L3-05 | Technical reference for developer summary and topic deep dives |
| [script-day-in-the-life.md](script-day-in-the-life.md) | 2–3 min | L1-01, L4-IL-*, L4-SB-* | Story reference for master explainer and micro-vignettes |
| [script-architectural-overview.md](script-architectural-overview.md) | 3–5 min | L2-03, L3-06, L3-07 | Architecture reference for standards body summary and composite stack deep dive |

## Reference Material: Originally Planned Batches (V-06 through V-20)

These were planned as 30-60 second vignettes under the original WO-0145 approach. Their content is now covered by the hierarchy system. Listed here for traceability.

| Original ID | Title | Now Covered By |
|-------------|-------|----------------|
| V-06 | Signatures and Integrity | L3-06 |
| V-07 | TTL and Offline Tolerance | L3-01 (within envelope deep dive) |
| V-08 | Forward Compatibility | L3-01, L3-06 |
| V-09 | Tamper Detection | L3-06 |
| V-10 | Expired Manifest Handling | L3-01 |
| V-11 | Smart Glasses and Privacy | L2-05, L4-IL-* |
| V-12 | Metaverse Portaling | L2-04, L3-04, L3-09 |
| V-13 | Proof of Personhood | L3-08, L4-IL-* |
| V-14 | Venue and Device Enrollment | L3-08, L4-IL-* |
| V-15 | Social Profile Portability | L3-08, L4-IL-* |
| V-16 | The Composite Stack | L3-07 |
| V-17 | Building Your First Manifest | L4-TL-* |
| V-18 | Adopting UM in Your Platform | L2-01, L2-02 |
| V-19 | UM vs. Other Standards | L2-03 |
| V-20 | The Consent Spectrum | L3-03 |

## Production Workflow (Updated)

### NotebookLM Pipeline (Primary)
1. **Brief** — ~500 char NotebookLM directive from [video-hierarchy-of-discovery.md](video-hierarchy-of-discovery.md)
2. **Knowledge vault** — NotebookLM has access to full UM spec, explainers, fixtures, and reference scripts
3. **Audio generation** — NotebookLM produces the audio content from the brief
4. **Visual production** — Motion graphics produced using reference scripts for visual direction
5. **Review** — Technical accuracy check against UM spec and fixtures
6. **Publish** — Upload to YouTube, embed in site, update UI links

### Visual Production Reference
- **Color palette:** Dark background (#0f172a), manifest glow (warm gold), facet accents (blue=profile, amber=claims, teal=consents, violet=devices, coral=pointers)
- **Typography:** Clean sans-serif (Inter or Geist)
- **Character roster:** Alex (creator), Riley (privacy guardian), Sam (developer/artist), Jordan (venue operator), Nova (metaverse character)
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels)

### YouTube Channel Structure (Updated)
- **Playlist: Start Here** — L0-01 (Welcome), L1-01 (Master Explainer)
- **Playlist: For Your Role** — L2-01 through L2-05 (Audience Summaries)
- **Playlist: Deep Dives** — L3-01 through L3-09 (Topic Explainers)
- **Playlist: Quick Demos** — L4-* (Micro-Vignettes, added as produced)
- **Each video:** Title, description with timestamps, tags (universal manifest, data portability, identity, privacy, consent, interoperability)
