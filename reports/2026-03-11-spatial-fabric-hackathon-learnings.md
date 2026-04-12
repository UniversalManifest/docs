# Spatial Fabric Hackathon Learnings Report

**Date:** 2026-03-11
**Work order:** WO-0150
**Prepared for:** OMA3 presentation (2026-03-12)

---

## 1. Executive Summary

On 2026-03-07, a proof-of-concept implementation was built during a hackathon to test whether Universal Manifest concepts work inside a real 3D spatial rendering environment. The implementation consisted of a portal server running on port 3333, a Manifest Commons API backend, and a Three.js WebGL browser that resolved Universal Manifests and projected avatar assets into a live 3D scene.

**What was proven:** UM's pointer-first, consent-aware, facet-based architecture works end-to-end in a spatial rendering context. Manifests stayed compact (under 3 KB), avatar GLBs (50+ MB) loaded externally via pointer URLs, dual-format normalization handled both UM v0.1 and Manifest Commons payloads, and identity traversal worked across three different consuming surfaces. The hackathon validated that UM is not a theoretical specification exercise — it is a buildable, deployable portable state contract.

**What this means for IWPS:** The portal concept demonstrated during the hackathon maps directly to the IWPS Query + Teleport flow. The UM manifest is the "cargo" for IWPS's "plumbing." The `assets` parameter in IWPS (currently TBD / Reserved for Future Use) could carry a UMID. Manifest resolution via `myum.net` provides the lookup that IWPS's Destination World needs to retrieve and validate portable state.

---

## 2. Architecture Demonstrated

The proof-of-concept implementation comprised four layers, each validating a different part of the UM specification's assumptions.

### Portal server

A bare Node.js HTTP server on port 3333 acted as the portal entry point. It accepted manifest references, performed dual-format normalization (UM v0.1 JSON-LD and Manifest Commons format), and returned a unified manifest shape to the rendering client. This validated UM's claim that manifests are format-portable and that consuming systems can normalize across schema variants without losing semantic meaning.

### Manifest Commons API

A TypeScript/Fastify service backed by Kysely ORM and MySQL provided the manifest storage and retrieval layer. Manifests were signed using Ed25519 keys with RFC 8785 (JCS) deterministic canonicalization. This validated UM's v0.2 signature profile assumptions in a production-grade persistence stack, not just in conformance test fixtures.

### Portal browser

A Three.js WebGL renderer loaded avatar GLB models from pointer URLs resolved out of the manifest envelope. The renderer consumed the `crossWorldProfile` facet, extracted avatar pointers by prefix, and loaded the referenced 3D models from external CDN and object-storage endpoints. This validated the pointer-first architecture under real rendering conditions: the manifest stayed lightweight while the heavy assets (50+ MB GLB files) loaded externally.

### ActivityPub integration

WebFinger discovery and federated identity endpoints were wired alongside the portal server. The same manifest that drove the Three.js renderer also served ActivityPub actor lookups, proving that a single UM envelope can serve multiple consuming protocols without per-protocol manifest variants.

---

## 3. UM Concepts Validated

### Pointer-first architecture

Manifests consistently stayed under 3 KB. Avatar GLBs — including the DamagedHelmet (4.2 MB), Lantern (7.5 MB), and Fox (3.3 MB) standard Khronos models — loaded from external CDN URLs referenced as pointer values. The manifest never attempted to carry binary asset data. This is the core UM design principle, and the hackathon proved it works under real rendering load without latency or payload-size problems.

### Dual-format normalization

The portal server accepted both UM v0.1 JSON-LD envelopes and Manifest Commons format documents. It normalized both to a common internal shape before passing them to the renderer. This proved that UM's envelope design is resilient to format variation: a consuming system does not need to hard-code a single schema version, and documents from different issuers can coexist in the same resolution pipeline.

### Cross-renderer identity traversal

The same manifest served three distinct consuming surfaces:

1. **Portal browser** (Three.js WebGL) — resolved avatar pointers and projected a 3D scene.
2. **RP1 spatial fabric** — consumed the manifest for spatial context binding and anchor resolution.
3. **ActivityPub endpoints** — served federated identity via WebFinger discovery.

No per-surface manifest variants were needed. Each consumer read the facets and pointers relevant to its capabilities and ignored the rest. This is exactly the behavior UM's facet model is designed to enable.

### Facet-based privacy

Consent toggles in the manifest controlled what each consuming surface was allowed to access. The portal browser enforced consent at runtime: when `metaverse.voiceCapture` was set to `denied`, the voice feature was not activated. Privacy boundaries traveled with the manifest, not with platform-specific configuration. This validated UM's default-deny consent propagation model in a real multi-surface deployment.

### TTL and freshness management

The Manifest Commons API re-stamped manifests every 30 minutes during the live demo session. Consuming surfaces checked `issuedAt` and `expiresAt` before projection. Stale manifests were rejected and re-fetched. This validated that UM's freshness model works in practice without requiring a complex revocation infrastructure — simple TTL-based validity is sufficient for live demo cadences and would scale to production refresh intervals.

### Identity fallback chains

The implementation used a four-level identity resolution chain:

1. **WebFinger** — federated discovery as first-class lookup.
2. **ActivityPub actor** — structured identity document from the federation layer.
3. **REST endpoint** — direct manifest retrieval from the Manifest Commons API.
4. **localStorage** — client-side cached state as the last-resort fallback.

This chain never hard-failed. If one level was unavailable, the next level provided continuity. This pattern validates UM's design assumption that identity resolution should be resilient and multi-path rather than dependent on a single authority.

---

## 4. Demo Manifests Used

The hackathon used four distinct manifests to test different format, facet, and asset combinations.

### Nova creator manifest

- **Identifier:** `urn:uuid:portal-demo-creator-001`
- **Format:** UM v0.1 JSON-LD
- **Avatar asset:** DamagedHelmet GLB (Khronos standard sample model)
- **Purpose:** Primary demo identity. Demonstrated creator-profile facets, avatar pointer resolution, and consent propagation in the Three.js renderer.

### Beacon spatial work manifest

- **Identifier:** `portal-demo-spatial-work-001`
- **Format:** Manifest Commons format (not UM v0.1)
- **Avatar asset:** Lantern GLB (Khronos standard sample model)
- **Purpose:** Tested dual-format normalization. The portal server accepted this non-UM-v0.1 document and normalized it to the same shape consumed by the renderer, proving format portability.

### XR avatar manifest

- **Identifier:** `urn:uuid:portal-demo-xr-avatar-001`
- **Format:** UM v0.1 JSON-LD
- **Avatar asset:** Fox GLB (Khronos standard sample model)
- **Purpose:** Tested XR-specific facets and avatar projection. Demonstrated that a manifest designed for spatial/XR use cases uses the same envelope as a creator-profile manifest.

### Track A Public Space manifest

- **Source:** External manifest from ai-scene-builder
- **Asset references:** 12+ asset pointers referencing scene elements, lighting, and environment objects
- **Purpose:** Stress-tested the pointer resolution pipeline with a higher pointer count. Proved that the resolver and renderer handle multi-asset manifests without degradation.

---

## 5. Gaps and Friction Discovered

The hackathon also surfaced real gaps and friction points that inform future UM specification work.

### Earth coordinate ownership blocker

The RP1 spatial fabric required coordinate ownership to deploy spatial objects at Earth-scale locations. The hackathon team did not own the relevant Earth coordinates, blocking direct deployment. The workaround was to deploy to Karona (an alternative RP1 coordinate space without ownership restrictions). This is not a UM specification gap, but it is a practical deployment friction that any real-world UM + spatial fabric integration will encounter. UM guidance should acknowledge that spatial deployment may require coordinate-level authorization beyond what the manifest carries.

### Overlay and property bypass rules undefined

The hackathon revealed that overlay composition rules (how multiple overlays from different sources combine or override each other) and property bypass rules (which manifest properties a consuming platform may override locally) are not defined in UM or in the metaverse integration lane. For the hackathon, the portal server used a simple last-write-wins strategy, but production deployments will need explicit precedence and conflict-resolution semantics.

### NSO service registration at unowned locations

The Network Service Object (NSO) concept from the spatial fabric requires service registration at specific spatial locations. When those locations are not owned by the manifest issuer, the registration path is unclear. This is an integration-lane gap: UM should document the expected behavior when a manifest references spatial services at locations the issuer does not control.

### Proximity event signaling undefined

The hackathon needed proximity-based events (triggering actions when a user approaches a spatial anchor or portal). No standard signaling mechanism exists for this. The implementation fell back to browser-side polling, which works for demos but does not scale. The open question is whether proximity signaling should be handled by the spatial fabric infrastructure, by an event broker, or by the client polling the spatial service. UM does not need to define this protocol, but the metaverse integration lane should acknowledge the gap and recommend that consuming platforms define their own proximity event model.

### Scene re-subscribe data recovery

A bug was encountered in the RP1 spatial fabric where re-subscribing to a scene after a disconnection did not fully recover the previous state. Some spatial objects were lost. This is a runtime bug in the spatial fabric implementation, not a UM specification issue, but it highlights the importance of UM's freshness and re-fetch model: consuming systems should be able to re-resolve the manifest and re-project from a clean state rather than depending on subscription continuity.

---

## 6. IWPS Alignment Implications

The hackathon results directly support the case for UM as the portable state layer that complements the Inter-World Portaling Standard (IWPS).

### UM is the cargo; IWPS is the plumbing

The hackathon proved that UM manifests can serve as the self-contained portable state envelope for a portal transition. The portal server on port 3333 effectively performed the same role as an IWPS Destination World: it received a manifest reference, resolved the manifest, validated freshness, read consent rules, resolved supported asset pointers, and projected the result into a rendering surface. This is exactly the IWPS Query + Teleport flow, implemented against UM manifests.

### The portal concept maps to IWPS Query + Teleport

The hackathon's portal flow followed a natural two-phase pattern:

1. **Query phase:** The portal browser sent a manifest reference to the portal server, which fetched and validated the manifest, checked consent, and determined which assets could be projected.
2. **Teleport phase:** The portal server returned the normalized manifest and resolved asset URLs to the renderer, which loaded the 3D scene.

This two-phase pattern is structurally identical to the IWPS Query + Teleport API. The hackathon demonstrated that this pattern works in practice without requiring IWPS-specific protocol implementation — the underlying semantic flow is the same.

### The `assets` parameter could carry a UMID

The hackathon used manifest identifiers (URN UUIDs) as the primary reference passed between the portal browser and the portal server. In an IWPS integration, this same identifier would be the value of the `assets` parameter in the Query and Teleport API calls. The IWPS specification marks `assets` as "Reserved for Future Use" — UM provides the structured, validated, consent-aware payload that this parameter is designed to carry.

### Manifest resolution provides IWPS Destination lookup

The Manifest Commons API served as the manifest resolver during the hackathon. In a production IWPS deployment, `myum.net/{UMID}` would serve the same function: the Destination World fetches the manifest from the resolver, validates it, and projects supported content. The resolver is the bridge between IWPS's transport-level reference and UM's full portable state envelope.

---

## 7. Patterns for Adoption

The hackathon produced several reusable patterns that inform how UM should be adopted in spatial and metaverse environments.

### Temporal event recording

The implementation maintained an append-only event log with asset references. Every portal resolution, avatar load, consent check, and freshness validation was recorded with a timestamp and a reference to the manifest and asset involved. This pattern is useful for audit trails, debugging, and compliance evidence in production deployments.

### Identity fallback chains

The four-level identity resolution chain (WebFinger, ActivityPub actor, REST endpoint, localStorage) proved that identity lookup should never hard-fail. Each level provides a degraded but functional identity surface. This pattern should be recommended in UM's integration guidance: consuming systems should implement at least two identity resolution paths and fall back gracefully when the primary path is unavailable.

### Manifest refresh cadence

The 30-minute re-stamping interval worked well for a live demo session. It was frequent enough to keep manifests valid during active use but infrequent enough to avoid unnecessary API load. For production deployments, the recommended refresh cadence will depend on the use case: high-frequency trading or real-time collaboration may need shorter intervals, while static profile portability may tolerate longer TTLs.

### External asset hosting

The hackathon used two asset hosting strategies:

- **Khronos CDN** for standard sample models (DamagedHelmet, Lantern, Fox) — publicly accessible, stable URLs, well-known formats.
- **MinIO object storage** for custom models — self-hosted, controllable access, suitable for assets that should not be publicly discoverable.

This dual-hosting pattern validates UM's pointer-first design: the manifest does not care where the asset lives, only that the pointer resolves to a valid resource. Asset hosting is an operational concern, not a specification concern.

### Facet extraction pattern

The portal browser used a consistent facet extraction pattern:

1. Switch on `facet.name` to identify the facet type.
2. For each recognized facet, extract pointer values by URI prefix.
3. Resolve pointers to external resources.
4. Project the resolved resources into the renderer.
5. Ignore unrecognized facets without error.

This pattern should be documented as a recommended consumer implementation approach. It is simple, resilient to unknown facets, and naturally supports graceful degradation.

---

## References

- Historical hackathon handoff notes were referenced during this writeup, but the corresponding `.dev` artifact is not present in the current checkout.
- [`integrations/metaverse.md`](../../integrations/metaverse.md) — UM metaverse integration lane
- [`integrations/rp1-spatial-fabric.md`](../../integrations/rp1-spatial-fabric.md) — RP1 spatial fabric integration lane
- [`docs/explainers/metaverse-portaling.md`](../explainers/metaverse-portaling.md) — MUM portaling explainer
- [`docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`](2026-03-06-omb-wiki-spatial-fabric-crosscheck.md) — OMB Wiki spatial fabric crosscheck
- [`docs/reports/2026-03-11-iwps-um-alignment-analysis.md`](2026-03-11-iwps-um-alignment-analysis.md) — IWPS-UM alignment analysis
- [`docs/journeys/journey-09-metaverse-crossworld-projection.md`](../journeys/journey-09-metaverse-crossworld-projection.md) — Metaverse portaling journey
