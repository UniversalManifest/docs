# Video Explainer Hierarchy of Discovery

**Status:** ACTIVE
**Work Order:** [WO-0149](../workorders/WO-0149-video-explainer-hierarchy-of-discovery.md)
**Last Updated:** 2026-03-11
**Production Pipeline:** NotebookLM briefs (this document) replace detailed scene-by-scene scripts.

---

## How This System Works

Universal Manifest video content is organized into a **hierarchy of discovery** — a layered system where different audiences find their entry point and drill down into detail at their own pace.

**Two standard lengths:**
- **Vignette** — 2 minutes. Focused, accessible, single-concept or audience-specific.
- **Deep Explainer** — 6 minutes. Comprehensive, technical, covers a topic end-to-end.

**Production pipeline:** Each video below has a NotebookLM brief — a short directive (~500 chars) that tells NotebookLM what to focus on and what to exclude. NotebookLM has access to the full UM knowledge vault (spec, explainers, fixtures, integration docs) and produces audio content from these briefs. The detailed scene-by-scene scripts from WO-0145 (V-01 through V-05) are retained as reference material for visual production, not as the primary production input.

**Terminology rules:**
- Use "facets" (not "shards") for modular data compartments.
- Frame UM as a specification, not an implementation.
- Use "OMATrust" for product/protocol references; "OMA3" for standards-body context.

---

## Level 0: Meta / Index

The entry point. Explains the hierarchy itself and directs viewers to the right starting video.

### L0-01: Welcome to Universal Manifest
**Level:** 0 | **Length:** 2 min
**Audience:** Anyone arriving for the first time — the YouTube channel trailer and site landing video.

**FOCUS:** Introduce Universal Manifest as a portable data specification. Explain that the video library is organized by audience and depth. Name the five audience paths (executives, developers, standards bodies, metaverse builders, privacy/compliance) and point each to their Level 2 summary. Mention that the Master Explainer (L1-01) covers everything in one video.

**DO NOT COVER:** Do not explain any technical concepts in depth — no JSON-LD, no facets, no signatures, no resolver mechanics. This video is a map, not a lesson. Do not mention PeerMesh or any specific implementation.

**WHY THIS EXISTS:** The single orientation point so no viewer ever feels lost about where to start.

---

## Level 1: Master Explainer

The one video someone watches if they only watch one. Covers all major concepts end-to-end.

### L1-01: Everything You Need to Know About Universal Manifest
**Level:** 1 | **Length:** 6 min
**Audience:** Anyone who wants the complete picture — potential adopters, conference attendees, curious technologists.

**FOCUS:** Cover the full UM story: the data fragmentation problem, the portable envelope concept (JSON-LD, UMID, TTL), facets and pointers as modular data architecture, default-deny consent model, manifest resolution via myum.net, cryptographic signatures (Ed25519 + JCS in v0.2), the composite stack (storage/transit/runtime), and real-world scenarios (gallery, smart glasses, metaverse portaling, proof of personhood). End with the adoption path.

**DO NOT COVER:** Do not go deep on any single integration lane — keep each scenario to one or two sentences. Do not discuss IWPS protocol details, specific standards body positioning, or implementation-level code. This is the complete map, not the territory.

**WHY THIS EXISTS:** The single canonical overview — replaces needing to watch multiple videos to get the full picture.

---

## Level 2: Audience-Specific Summaries

Different paths for different people. Each summary covers the same specification but emphasizes what matters to that audience.

### L2-01: Universal Manifest for Executives and Decision Makers
**Level:** 2 | **Length:** 2 min
**Audience:** CTOs, product leaders, business strategists evaluating UM for adoption.

**FOCUS:** The business case: data fragmentation costs (custom integrations, duplicated effort, compliance burden), how UM reduces integration cost with one portable format, competitive positioning vs. VCs/DIDComm/Solid/OIDC, native privacy compliance (default-deny consent travels with data), and the progressive adoption path (parse, validate, consume, issue, sign). Emphasize that UM is a specification, not a vendor product.

**DO NOT COVER:** Do not explain JSON-LD structure, facet internals, pointer mechanics, or cryptographic details. Do not mention specific fixture names, schema files, or TypeScript. No metaverse portaling or smart glasses scenarios — keep it boardroom-relevant.

**WHY THIS EXISTS:** Gives decision makers the value proposition and competitive landscape without technical detail.

---

### L2-02: Universal Manifest for Developers and Integrators
**Level:** 2 | **Length:** 2 min
**Audience:** Software engineers, system architects, API integrators evaluating UM for technical adoption.

**FOCUS:** The data structures: JSON-LD document format, UMID as UUID URN, issuedAt/expiresAt TTL, facets as named modular sections, pointers as URI references to authoritative data. Consuming a manifest: JSON parsing, JSON Schema validation, facet reading, consent checking. The resolver at myum.net/{UMID}. Forward compatibility (ignore unknown fields). The adoption ladder from Level 1 (parse JSON) through Level 5 (sign and verify). Mention the TypeScript reference implementation exists as one option.

**DO NOT COVER:** Do not cover business value propositions, competitive positioning, or standards body politics. Do not explain specific integration lanes (metaverse, smart glasses, venue enrollment) — those are Level 3. Do not frame UM as a TypeScript library.

**WHY THIS EXISTS:** Gives developers the technical mental model to start integrating without needing the full spec.

---

### L2-03: Universal Manifest for Standards Bodies
**Level:** 2 | **Length:** 2 min
**Audience:** OMA3, W3C, Metaverse Standards Forum participants, and governance-focused evaluators.

**FOCUS:** Architectural positioning: UM as a portable state envelope specification that complements (not replaces) existing standards. How UM relates to W3C Verifiable Credentials (UM carries VCs as claims within facets), DIDComm (UM is a document format, DIDComm is a messaging protocol), Solid (UM uses pointers to Solid Pods), and OIDC (UM carries broader state). The IWPS complementarity: UM provides the portable identity and consent layer, IWPS provides the inter-world transport protocol. The spec-vs-implementation boundary: UM is language-neutral, JSON Schema validated, with open-source governance.

**DO NOT COVER:** Do not explain how to build or parse a manifest. Do not cover user-facing scenarios (gallery, smart glasses). Do not discuss the TypeScript reference implementation or npm packages. Keep it at the standards architecture level.

**WHY THIS EXISTS:** Positions UM in the standards landscape so evaluators understand where it fits without implementation details.

---

### L2-04: Universal Manifest for Metaverse Builders
**Level:** 2 | **Length:** 2 min
**Audience:** Virtual world developers, XR platform architects, spatial computing teams.

**FOCUS:** Cross-world identity portability: one manifest carries avatar, display name, social graph, and achievements across virtual worlds. Portaling: how a manifest travels through a portal from World A to World B with identity intact. The crossWorldProfile facet and metaverse pointers (avatar assets, social graph, achievements). Consent controls for metaverse contexts (voice capture, face visibility, profile publicity). How UM + IWPS together form the complete portaling stack — UM handles identity/consent, IWPS handles transport.

**DO NOT COVER:** Do not explain the full UM specification, JSON-LD details, or the resolver system. Do not cover non-metaverse scenarios (galleries, smart glasses privacy, device enrollment). Do not discuss standards body governance or business ROI.

**WHY THIS EXISTS:** Shows metaverse builders exactly how UM solves cross-world identity without needing the full spec context.

---

### L2-05: Universal Manifest for Privacy and Compliance
**Level:** 2 | **Length:** 2 min
**Audience:** Privacy officers, compliance teams, data protection evaluators, regulators.

**FOCUS:** The default-deny consent model: nothing is shared unless explicitly granted. Consent travels inside the manifest, so every downstream system knows what it can and cannot do without calling back. Facet-level controls: each data compartment can have independent consent settings. Smart glasses scenario as a privacy exemplar (face visibility, voice recording — denied by default). Offline tolerance: TTL-based expiry means no revocation infrastructure needed, reducing data-retention surface. How UM aligns with privacy-by-design principles.

**DO NOT COVER:** Do not explain JSON-LD, data structures, resolver mechanics, or cryptographic signatures. Do not cover metaverse portaling, developer adoption paths, or competitive positioning against other standards. Keep it focused on the privacy and consent architecture.

**WHY THIS EXISTS:** Demonstrates to privacy stakeholders that consent is structural, not an afterthought bolted on top.

---

## Level 3: Topic Deep Dives

Detailed coverage of specific concepts. These are standalone explainers designed to be embedded alongside documentation pages.

### L3-01: The Portable Envelope
**Level:** 3 | **Length:** 6 min
**Audience:** Anyone wanting to deeply understand the core manifest structure.

**FOCUS:** The complete anatomy of a Universal Manifest document. JSON-LD as the base format: @context for semantic richness, valid JSON for universal parsing. The UMID: UUID URN format, globally unique, offline-generatable, resolvable at myum.net. The subject field: DID or URI identifying who/what the manifest is about. TTL mechanics: issuedAt and expiresAt timestamps, validity window checking, why expired means rejected (no renewal mechanism). The minimal valid manifest (~300 bytes). How the envelope stays lightweight (1-3 KB typical) by using pointers instead of embedding data.

**DO NOT COVER:** Do not explain facet internals, consent model, signatures, or the resolver in depth — those are separate L3 videos. Do not cover specific use cases or integration scenarios. Stay on the envelope itself.

**WHY THIS EXISTS:** The definitive explanation of the manifest document structure, separate from what goes inside it.

---

### L3-02: Facets and Pointers
**Level:** 3 | **Length:** 6 min
**Audience:** Developers and architects wanting to understand UM's modular data architecture.

**FOCUS:** Facets as named, typed data compartments within the manifest. Well-known facet names: publicProfile, deviceIdentity, venuePolicy, crossWorldProfile, gameProfile. How facets are arrays of objects with @type and name fields. Pointers: URI references to authoritative external data instead of copying it. Why pointers keep manifests small and avoid stale-copy problems. Pointer names: solidPod.creatorCanonical, matrix.userId, activityPub.actor, metaverse.avatar, metaverse.socialGraph. The difference between a facet (data inside the manifest) and a pointer (reference to data outside). Extensibility: defining custom facets for new use cases.

**DO NOT COVER:** Do not cover consent mechanics, signatures, resolution, or the envelope structure — those are separate L3 videos. Do not discuss specific integration lane scenarios beyond brief examples.

**WHY THIS EXISTS:** The definitive explanation of how data is organized and referenced inside a manifest.

---

### L3-03: Default-Deny Consent
**Level:** 3 | **Length:** 6 min
**Audience:** Anyone wanting to deeply understand UM's privacy model.

**FOCUS:** The consent architecture: consents as an array of objects with @type, name, and value. The four states: allowed (green), denied (red), restricted (amber), and not-set (treated as denied). Default-deny principle: if a consent is absent, the answer is no. How consent travels inside the manifest so downstream systems enforce it without calling back. Facet-level consent granularity: different permissions for different data compartments. Real examples: publicDisplay allowed, analytics.tracking denied, ar.recording.faceVisible not-set (therefore denied). How consuming systems check consent before accessing facet data.

**DO NOT COVER:** Do not explain the envelope structure, pointer mechanics, signatures, or resolution. Do not go deep on specific integration lanes — use brief examples only. Do not discuss compliance frameworks by name (GDPR, CCPA) — stay on the UM consent architecture itself.

**WHY THIS EXISTS:** The definitive explanation of how consent works as a structural, portable, default-deny system.

---

### L3-04: Cross-World Identity and Portaling
**Level:** 3 | **Length:** 6 min
**Audience:** Metaverse developers and XR architects wanting the full portaling story.

**FOCUS:** The cross-world identity problem: re-registration, lost progress, fragmented social graphs across virtual worlds. How UM solves it: the crossWorldProfile facet carries avatar preferences, display name, and achievements. Metaverse pointers (metaverse.avatar, metaverse.socialGraph, metaverse.achievements) reference authoritative assets without copying them. The portaling flow: user enters a portal in World A, their manifest UMID travels to World B, World B resolves the manifest, reads the crossWorldProfile facet, loads avatar from pointer, checks metaverse consent toggles. The UM + IWPS relationship: UM provides the identity/consent envelope, IWPS provides the inter-world transport protocol. Together they form the complete portaling stack.

**DO NOT COVER:** Do not explain the general UM envelope, consent model in full, or signature mechanics — those are separate L3 videos. Do not cover non-metaverse scenarios. Do not describe IWPS protocol internals beyond the complementarity relationship.

**WHY THIS EXISTS:** The definitive explanation of how manifests enable persistent identity across virtual worlds.

---

### L3-05: Manifest Resolution
**Level:** 3 | **Length:** 6 min
**Audience:** Developers and integrators wanting to understand the resolver system.

**FOCUS:** The resolution problem: how does a consumer get a manifest when they only have a UMID? The myum.net resolver: a lookup service where manifests are published and fetched by UMID. The publish flow: issuer pushes manifest to myum.net. The resolve flow: consumer sends UMID to myum.net/{UMID}, receives the manifest. Always-current guarantee: the resolver serves the latest published version. Transport agnosticism: manifests can also be shared via QR code, Bluetooth, API call, or file transfer — the resolver is one option, not the only path. How resolution fits into the validate-then-consume lifecycle. The provenance chain: fetched manifest still requires TTL check, signature verification, and consent checking by the consumer.

**DO NOT COVER:** Do not explain the manifest structure, facets, consent model, or signatures in depth — reference them briefly. Do not discuss resolver implementation details (Cloudflare Workers, caching strategy). Stay at the specification level.

**WHY THIS EXISTS:** The definitive explanation of how manifests are published and looked up across the network.

---

### L3-06: Signatures and Integrity
**Level:** 3 | **Length:** 6 min
**Audience:** Security-minded developers and architects wanting the trust model.

**FOCUS:** The tamper-detection problem: how does a consumer know a manifest has not been modified in transit? The v0.2 signature profile: JCS (JSON Canonicalization Scheme, RFC 8785) for deterministic serialization, Ed25519 for compact and fast cryptographic signatures. The signing flow: canonicalize the manifest payload with JCS, sign with the issuer's Ed25519 private key, embed the signature block in the manifest. The verification flow: extract the signature, re-canonicalize the payload, verify with the issuer's public key. Modular signature profiles: consumers verify the profiles they support, safely ignore unknown ones — forward compatibility. What signatures do not cover: they prove integrity and issuer identity, not consent or freshness (those are separate checks).

**DO NOT COVER:** Do not explain the full manifest structure, facets, consent, or resolution — reference briefly. Do not discuss specific key management infrastructure, PKI choices, or DID method details. Do not cover v0.1 (which has no signature support).

**WHY THIS EXISTS:** The definitive explanation of how cryptographic integrity works in UM v0.2.

---

### L3-07: The Composite Stack Architecture
**Level:** 3 | **Length:** 6 min
**Audience:** System architects and technical leaders wanting to understand where UM fits.

**FOCUS:** The three-layer composite stack: Storage/Registry (Solid Pods, databases, canonical data stores), Transit/State Envelope (Universal Manifest), and Execution/Runtime (web apps, native clients, spatial engines, edge devices). UM is the transit layer — it does not replace storage and it does not replace runtime. It bridges them by securely carrying identity, pointers, and consents from storage into execution. How each layer has its own responsibilities and UM only claims the transit role. Integration patterns: read-only consumption, bidirectional publishing, full lifecycle management. Why this separation matters: existing storage and runtime investments are preserved, UM just standardizes the handoff.

**DO NOT COVER:** Do not explain specific data structures, consent mechanics, or signature details — those are separate L3 videos. Do not discuss specific implementations or runtime frameworks. Do not cover IWPS or metaverse-specific architecture.

**WHY THIS EXISTS:** The definitive explanation of UM's architectural position in a system stack.

---

### L3-08: Integration Lanes Overview
**Level:** 3 | **Length:** 6 min
**Audience:** Product managers and integrators evaluating which UM integration paths are relevant.

**FOCUS:** Survey of all major integration lanes: gallery/venue display (manifest-driven art display with consent and content policy), smart glasses (AR/XR consent enforcement for recording and face visibility), metaverse portaling (cross-world identity via IWPS + UM), proof of personhood (multi-provider human verification without personal data exposure), social profile portability (one profile across platforms), device enrollment (edge devices auto-configure from manifest policies), and professional credentials (portable licenses and certifications). For each lane: the problem it solves, which facets/consents are involved, and the current status (proven in fixtures vs. conceptual).

**DO NOT COVER:** Do not go deep on any single lane — each gets approximately 45 seconds. Do not explain the underlying data structures or consent mechanics in detail. Do not discuss implementation specifics or code. This is the menu, not the meal.

**WHY THIS EXISTS:** The single survey of all integration possibilities so evaluators can identify which lanes matter to them.

---

### L3-09: IWPS + UM: The Complete Portaling Stack
**Level:** 3 | **Length:** 6 min
**Audience:** Standards-aware metaverse architects wanting to understand the full portaling architecture.

**FOCUS:** The two-layer portaling architecture: IWPS (Inter-World Portaling System) handles the transport protocol for moving between virtual worlds, UM handles the portable identity, consent, and credential envelope that travels through the portal. How they complement each other: IWPS defines how a portal connection is established and how data flows between worlds; UM defines what data the user carries and what permissions govern it. The handoff: IWPS initiates the portal, requests the user's UMID, UM manifest is resolved and delivered to the destination world. Consent enforcement at the destination: the receiving world reads UM consent toggles before rendering avatar, loading social graph, or capturing voice/face. Why neither layer alone is sufficient — IWPS without UM has no portable identity; UM without IWPS has no transport mechanism.

**DO NOT COVER:** Do not explain UM data structures or consent model in depth — reference them. Do not cover non-portaling UM use cases. Do not discuss IWPS protocol internals (handshake, packet format) beyond the conceptual architecture. Do not position this as UM-vs-IWPS — they are partners.

**WHY THIS EXISTS:** The definitive explanation of how UM and IWPS together solve the metaverse portaling problem.

---

## Level 4: Micro-Vignettes

Short, focused pieces designed for embedding on specific documentation pages. These are produced as needed when documentation pages are ready for video embeds.

### L4-SB: Per-Sandbox-Scenario Vignettes
**Level:** 4 | **Length:** 2 min each
**Audience:** Documentation site visitors exploring sandbox scenarios.

**FOCUS per vignette:** Each covers one sandbox scenario category. Getting Started scenarios (creating a minimal manifest, adding consents, adding facets, resolving by UMID). Trust and Verification scenarios (signature validation, tamper detection, expired manifest handling, forward compatibility). Integration Lane scenarios (gallery display, smart glasses, metaverse portaling, proof of personhood, device enrollment).

**DO NOT COVER:** Do not repeat the Level 3 deep dive content. Each micro-vignette should be a focused walkthrough of what happens in that specific scenario, not a concept explanation.

**WHY THIS EXISTS:** Page-level embeds that make sandbox scenarios immediately understandable before interacting.

---

### L4-IL: Per-Integration-Lane Vignettes
**Level:** 4 | **Length:** 2 min each
**Audience:** Documentation site visitors exploring specific integration lanes.

**FOCUS per vignette:** Each covers one integration lane in a concrete, scenario-driven format. Gallery/venue display: artist walks in, art appears on screens. Smart glasses: bystander's consent is checked and enforced. Metaverse portaling: user leaps between worlds with identity intact. Proof of personhood: user is verified without exposing personal data. Social portability: user joins a new platform with profile pre-filled. Device enrollment: new display auto-configures from venue manifest.

**DO NOT COVER:** Do not explain the underlying specification mechanics. Each vignette is a story, not a tutorial. Do not reference other integration lanes within a single vignette.

**WHY THIS EXISTS:** Concrete scenario demonstrations embedded alongside integration lane documentation pages.

---

### L4-TL: Per-Tool Vignettes
**Level:** 4 | **Length:** 2 min each
**Audience:** Developers using UM tools (workbench, harness, validator).

**FOCUS per vignette:** Each covers one tool. The interactive harness: how to load fixtures, step through scenarios, inspect manifest state. The sandbox workbench: how to create and edit manifests interactively. The validator: how to check a manifest against the JSON Schema.

**DO NOT COVER:** Do not explain UM concepts — assume the viewer already understands the specification. Focus purely on tool usage and workflow.

**WHY THIS EXISTS:** Quick tool walkthroughs so developers can start using UM tooling immediately.

---

## Video ID Summary

| ID | Title | Level | Length | Audience |
|----|-------|-------|--------|----------|
| L0-01 | Welcome to Universal Manifest | 0 | 2 min | Everyone |
| L1-01 | Everything You Need to Know About UM | 1 | 6 min | Everyone |
| L2-01 | UM for Executives | 2 | 2 min | Decision makers |
| L2-02 | UM for Developers | 2 | 2 min | Engineers, integrators |
| L2-03 | UM for Standards Bodies | 2 | 2 min | OMA3, W3C, MSF |
| L2-04 | UM for Metaverse Builders | 2 | 2 min | XR/virtual world devs |
| L2-05 | UM for Privacy and Compliance | 2 | 2 min | Privacy officers, regulators |
| L3-01 | The Portable Envelope | 3 | 6 min | Technical deep dive |
| L3-02 | Facets and Pointers | 3 | 6 min | Technical deep dive |
| L3-03 | Default-Deny Consent | 3 | 6 min | Technical deep dive |
| L3-04 | Cross-World Identity and Portaling | 3 | 6 min | Technical deep dive |
| L3-05 | Manifest Resolution | 3 | 6 min | Technical deep dive |
| L3-06 | Signatures and Integrity | 3 | 6 min | Technical deep dive |
| L3-07 | The Composite Stack Architecture | 3 | 6 min | Technical deep dive |
| L3-08 | Integration Lanes Overview | 3 | 6 min | Technical deep dive |
| L3-09 | IWPS + UM: The Complete Portaling Stack | 3 | 6 min | Technical deep dive |
| L4-SB-* | Sandbox Scenario Vignettes | 4 | 2 min each | Doc site visitors |
| L4-IL-* | Integration Lane Vignettes | 4 | 2 min each | Doc site visitors |
| L4-TL-* | Tool Vignettes | 4 | 2 min each | Developers |

**Total named videos:** 16 (Levels 0-3) + open-ended micro-vignettes (Level 4)
**Total runtime (Levels 0-3):** ~66 minutes (2 vignettes at 2 min + 1 master at 6 min + 5 summaries at 2 min + 9 deep dives at 6 min)

---

## Relationship to WO-0145 Scripts

The detailed scene-by-scene scripts produced under WO-0145 (V-01 through V-05) and the five long-form scripts remain as **reference material** for:
- Visual production: scene descriptions, character assignments, color palettes, and motion-graphics direction.
- Content accuracy: technical details, fixture references, and spec-aligned terminology.
- NotebookLM context: uploaded to the knowledge vault alongside the spec and explainer documents.

These scripts are **not** the direct production input. The NotebookLM briefs in this document are the production directives.

| WO-0145 Script | Maps To |
|----------------|---------|
| script-what-is-um.md | L1-01, L3-01, L3-02 |
| script-why-it-matters.md | L2-01, L3-08, L4-IL-* |
| script-how-it-works.md | L2-02, L3-01, L3-02, L3-03, L3-05 |
| script-day-in-the-life.md | L1-01, L4-IL-*, L4-SB-* |
| script-architectural-overview.md | L2-03, L3-06, L3-07 |
| V-01 (Portable Envelope) | L3-01 |
| V-02 (Facets and Pointers) | L3-02 |
| V-03 (Default-Deny Consent) | L3-03 |
| V-04 (Cross-World Identity) | L3-04 |
| V-05 (Manifest Resolution) | L3-05 |
