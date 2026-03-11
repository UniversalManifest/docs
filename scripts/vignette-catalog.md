# Vignette Video Library — Catalog

**Status:** DRAFT
**Work Order:** [WO-0145](../workorders/WO-0145-vignette-video-library.md)
**Last Updated:** 2026-03-11

This catalog tracks all planned vignette explainer videos for the Universal Manifest project. Each vignette is a standalone 30–60 second animated explainer designed for embedding in the documentation site UI and publishing on YouTube.

## Design Principles

- **UM-pure:** Every script explains Universal Manifest as a standalone specification. No PeerMesh, no implementation-specific branding.
- **Standalone:** Each vignette is self-contained. A viewer can watch any single video and learn one clear concept.
- **Fixture-grounded:** Visual examples reference real UM data structures, fixture patterns, and conformance behaviors.
- **Consistent visual language:** Dark background (#0f172a), warm gold manifest glow, accent colors per facet type. Same character roster as long-form scripts (Alex, Riley, Sam, Jordan, Nova).
- **Standard format:** 30–60 seconds, 16:9 primary with 1:1 and 9:16 derivatives.

## UI Placement Plan

Since the site currently has no video embeds, vignettes will be introduced as:
1. **Sandbox scenario pages** — A "Watch the explainer" link above each scenario category (Getting Started, Trust & Verification, Integration Lanes).
2. **Concept pages** — Embedded at the top of key docs pages (Overview, Spec, Integrations, Adoption Guide).
3. **Landing page** — Featured hero vignette on the site root.
4. **YouTube playlist** — All vignettes published as a sequential playlist with chapter markers.

---

## Batch 1 — Core Concepts (Priority: HIGHEST)

These 5 vignettes cover the foundational UM architecture. Scripted and ready for production.

| ID | Title | Duration | Script | Concept | UI Target |
|----|-------|----------|--------|---------|-----------|
| V-01 | The Portable Envelope | 30–45s | [vignette-01-portable-envelope.md](vignette-01-portable-envelope.md) | What a Universal Manifest is — the JSON-LD state capsule with UMID and TTL | Landing page hero, Overview page, Sandbox Getting Started |
| V-02 | Facets and Pointers | 30–45s | [vignette-02-facets-and-pointers.md](vignette-02-facets-and-pointers.md) | Modular data compartments with lightweight external references | Spec page, Sandbox GS-03 |
| V-03 | Default-Deny Consent | 30–45s | [vignette-03-default-deny-consent.md](vignette-03-default-deny-consent.md) | Privacy controls that travel inside the manifest | Adoption Guide, Sandbox GS-02 consent scenarios |
| V-04 | Cross-World Identity | 30–45s | [vignette-04-cross-world-identity.md](vignette-04-cross-world-identity.md) | Same identity across platforms, renderers, and virtual worlds | Metaverse integration page, Sandbox IL scenarios |
| V-05 | Manifest Resolution | 30–45s | [vignette-05-manifest-resolution.md](vignette-05-manifest-resolution.md) | How the resolver delivers manifests by UMID from anywhere | Resolver API page, Sandbox GS-04 |

## Batch 2 — Trust and Verification (Priority: HIGH)

| ID | Title | Duration | Script | Concept | UI Target |
|----|-------|----------|--------|---------|-----------|
| V-06 | Signatures and Integrity | 30–45s | — | Ed25519 + JCS canonicalization for tamper detection (v0.2) | Trust & Verification sandbox category |
| V-07 | TTL and Offline Tolerance | 30–45s | — | How expiration timestamps enable caching without revocation checks | Edge/IoT integration pages |
| V-08 | Forward Compatibility | 30–45s | — | Unknown fields are preserved, not rejected — future-proof by design | Spec versioning page, Sandbox GS-03 |
| V-09 | Tamper Detection | 30–45s | — | What happens when a manifest is modified in transit | Sandbox TV-02 |
| V-10 | Expired Manifest Handling | 30–45s | — | How consuming systems handle TTL expiry gracefully | Sandbox TV-03 |

## Batch 3 — Integration Lanes (Priority: MEDIUM)

| ID | Title | Duration | Script | Concept | UI Target |
|----|-------|----------|--------|---------|-----------|
| V-11 | Smart Glasses and Privacy | 30–45s | — | AR/XR consent enforcement for recording and face visibility | Smart Glasses integration page |
| V-12 | Metaverse Portaling | 30–45s | — | Portal-based movement between virtual worlds with manifest continuity | Metaverse/Portaling explainer page |
| V-13 | Proof of Personhood | 30–45s | — | Multi-provider human verification without exposing personal data | Personhood integration page |
| V-14 | Venue and Device Enrollment | 30–45s | — | How venues and edge devices auto-configure from manifest policies | Venue integration page |
| V-15 | Social Profile Portability | 30–45s | — | One profile across social platforms, no duplicate forms | Social integration page |

## Batch 4 — Advanced and Adopter-Facing (Priority: MEDIUM)

| ID | Title | Duration | Script | Concept | UI Target |
|----|-------|----------|--------|---------|-----------|
| V-16 | The Composite Stack | 30–45s | — | Storage/Transit/Runtime architecture — where UM fits | Architecture overview page |
| V-17 | Building Your First Manifest | 45–60s | — | Hands-on walkthrough of creating a minimal valid manifest | Sandbox Getting Started, Build Your Own page |
| V-18 | Adopting UM in Your Platform | 45–60s | — | Decision tree for integration: read-only, publish, or full | Adoption Guide page |
| V-19 | UM vs. Other Standards | 30–45s | — | How UM relates to VCs, DIDComm, Solid, OIDC | Standards Comparison page |
| V-20 | The Consent Spectrum | 30–45s | — | Allowed, denied, restricted, not-set — the full consent model | Consent deep-dive page |

## Existing Long-Form Scripts (Reference)

These scripts are already written and serve as source material for vignette adaptation:

| Script | Duration | Relationship to Vignettes |
|--------|----------|---------------------------|
| [script-what-is-um.md](script-what-is-um.md) | 60–90s | Covers V-01 through V-05 in narrative form |
| [script-why-it-matters.md](script-why-it-matters.md) | 60–90s | Contains 5 micro-stories that map to V-11, V-12, V-13, V-14 |
| [script-how-it-works.md](script-how-it-works.md) | 90–120s | Technical walkthrough — maps to V-02, V-03, V-05, V-06 |
| [script-day-in-the-life.md](script-day-in-the-life.md) | 2–3 min | Day narrative — maps to V-01, V-03, V-04, V-15 |
| [script-architectural-overview.md](script-architectural-overview.md) | 3–5 min | Architecture presentation — maps to V-16, V-02, V-06 |

## Production Workflow

### Format Specifications
- **Duration:** 30–60 seconds per vignette
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels)
- **Style:** Motion graphics / animated explainer
- **Color palette:** Dark background (#0f172a), manifest glow (warm gold), facet accents (blue=profile, amber=claims, teal=consents, violet=devices, coral=pointers)
- **Typography:** Clean sans-serif (Inter or Geist)
- **Audio:** Electronic track, UI sound effects per interaction (click, lock, chime, whoosh)

### Production Pipeline
1. **Script** — Written and reviewed (this catalog + individual script files)
2. **Storyboard** — Visual scene-by-scene breakdown with layout sketches
3. **Voiceover** — Record narration from speaker notes
4. **Animation** — Motion graphics production from storyboard
5. **Sound design** — Music bed + UI sound effects
6. **Review** — Technical accuracy check against UM spec and fixtures
7. **Publish** — Upload to YouTube, embed in site, update UI links

### YouTube Channel Structure
- **Playlist: Core Concepts** — V-01 through V-05
- **Playlist: Trust & Verification** — V-06 through V-10
- **Playlist: Integration Lanes** — V-11 through V-15
- **Playlist: Advanced Topics** — V-16 through V-20
- **Each video:** Title, description with timestamps, tags (universal manifest, data portability, identity, privacy, consent, interoperability)
