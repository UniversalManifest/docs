# Avatar Equip Tool — Gamified Universal Manifest Management Concept

> **Status:** Concept
> **Work Order:** [WO-0151](../workorders/WO-0151-avatar-equip-tool-concept.md)
> **Date:** 2026-03-11

---

## 1. Vision

The Avatar Equip Tool is a gamified visual interface for building and managing a Universal Manifest. It draws direct inspiration from AAA game equip menus — the kind found in RPGs and MMOs where players attach gear, weapons, and accessories to character slots on a paper-doll screen.

The core experience: a user brings in their 3D avatar, and "equips" data elements to it. Each slot on the avatar corresponds to a facet, pointer, claim, consent, or other UM primitive. Equipping an item adds it to the manifest; unequipping removes or revokes it.

The twist is that the equip menu is not limited to game items. The slots can hold an endless variety of things:

- Verifiable credentials and proof-of-personhood attestations
- Consent settings and privacy boundaries
- Pointers to 3D assets, portfolios, social graphs, and external data
- Compliance proofs (age verification, KYC)
- Payment handles (Stripe, PayPal, crypto wallet addresses)
- Device registrations (smart glasses, displays, hardware tokens)
- Encryption and projection settings for per-facet privacy control

This becomes the consumer's primary way to build, maintain, and understand their Universal Manifest — turning a JSON-LD specification artifact into something tactile, visual, and immediately comprehensible.

---

## 2. Core Metaphor

The avatar is the visual anchor. It represents the user's identity — their `subject` in UM terms.

**Equipment slots map to UM facets and pointers.** Each slot has a type (profile, credential, consent, pointer, claim, device, etc.). The user drags items into slots, and the manifest updates in real time underneath.

| Action in the UI | Effect on the Manifest |
|-------------------|----------------------|
| Equip an item to a slot | Add a facet, pointer, claim, or consent entry |
| Unequip an item | Remove or revoke the corresponding entry |
| Lock a slot | Mark the facet as encrypted / private |
| Inspect a slot | View the raw UM primitive (facet JSON, pointer URL, consent value) |
| Drag between slots | Reclassify or restructure data within the manifest |
| Export | Generate a valid, signed Universal Manifest JSON-LD document |

The visual representation makes complex data relationships intuitive. A user does not need to understand JSON-LD, JCS canonicalization, or Ed25519 signatures to build a complete, spec-conformant manifest. They just equip their avatar.

---

## 3. Architecture

### Separation from the UM Spec

The Avatar Equip Tool lives in a **separate repository**. It is not part of the Universal Manifest specification. It is a consumer application built ON the spec — reading and writing manifests that conform to the published UM contract.

This separation is critical: the UM specification must remain language-neutral and implementation-agnostic. The equip tool is one consumer of that specification, not a normative part of it.

### Component Overview

```
┌──────────────────────────────────────────────────────────┐
│  Avatar Equip Tool (separate repo)                       │
│                                                          │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │ Avatar Loader │  │ Equip Engine │  │ Manifest I/O  │  │
│  │              │  │              │  │               │  │
│  │ GLB/glTF     │  │ Drag & drop  │  │ UM v0.1/v0.2 │  │
│  │ import from  │  │ slot mgmt    │  │ parser &      │  │
│  │ pointer URLs │  │ category     │  │ generator     │  │
│  │              │  │ mapping      │  │               │  │
│  └──────┬───────┘  └──────┬───────┘  └───────┬───────┘  │
│         │                 │                   │          │
│         └────────┬────────┘                   │          │
│                  │                            │          │
│         ┌────────▼────────┐          ┌────────▼────────┐ │
│         │ 3D Renderer     │          │ Resolver Client │ │
│         │ (Three.js or    │          │ (myum.net)      │ │
│         │  equivalent)    │          │ publish / fetch │ │
│         └─────────────────┘          └─────────────────┘ │
│                                                          │
│         ┌─────────────────────────────────────────────┐  │
│         │ Crypto Module                               │  │
│         │ Ed25519 signing, JCS canonicalization,      │  │
│         │ per-facet encryption/decryption              │  │
│         └─────────────────────────────────────────────┘  │
│                                                          │
└──────────────────────────────────────────────────────────┘
         │                          │
         ▼                          ▼
  UM Specification            myum.net Resolver
  (spec/v0.1, v0.2)          (publish & fetch)
```

### Key Architectural Properties

- **UM spec consumer** — reads and writes manifests using the published UM specification (v0.1 and v0.2). The tool is conformant, not normative.
- **Resolver-aware** — can publish manifests to and fetch manifests from `myum.net/{UMID}`.
- **Avatar loader** — imports 3D avatars from pointer URLs (GLB/glTF format). The avatar model is itself a pointer in the manifest (`metaverse.avatar`).
- **Equip engine** — visual drag-and-drop interface for facet, pointer, claim, consent, and device management.
- **Crypto module** — handles Ed25519 signing (v0.2), JCS canonicalization, and per-facet encryption/decryption for private data slots.
- **Export** — generates valid Universal Manifest JSON-LD documents that pass conformance validation.

---

## 4. Equip Categories (Mapped to UM Primitives)

Each equip category maps directly to a UM structural primitive. The user sees intuitive category names; the manifest sees spec-conformant data structures.

| Equip Category | UM Primitive | Examples |
|----------------|-------------|----------|
| **Identity** | `crossWorldProfile` facet | Display name, bio, home world, avatar URL |
| **Credentials** | `claims` facet | Creator badge, verification stamps, proof-of-personhood |
| **Permissions** | `consents` array | Public display, analytics tracking, face recording, voice capture |
| **Inventory** | `pointers` | 3D assets, portfolio items, collectibles, wearables |
| **Social** | `socialGraph` pointer | Friends list, reputation scores, trust graph links |
| **Compliance** | Compliance facets | Age verification, KYC proofs, regulatory attestations |
| **Payments** | Payment handle facets | Stripe, PayPal, crypto wallet addresses, fiat/crypto gateways |
| **Devices** | `deviceRegistration` facet | Enrolled hardware, smart glasses, displays, hardware tokens |
| **Privacy** | Encryption/projection settings | Which facets are encrypted, which are projected externally, per-facet visibility |

### Slot Interaction Model

Each slot in the UI displays:

1. **Category icon** — visual indicator of the slot type
2. **Equipped item summary** — human-readable label of what is attached
3. **Privacy indicator** — locked (encrypted), unlocked (public), or restricted (consent-gated)
4. **Pointer health** — for pointer-based slots, whether the external target is reachable
5. **Inspect action** — reveals the underlying UM primitive (facet JSON, pointer URL, consent value)

---

## 5. Why This Matters for the Spec

The Avatar Equip Tool is not just a consumer product concept. It is a **spec completeness forcing function**. Building a consumer interface on top of the UM specification will expose gaps, ambiguities, and friction points that pure document-level analysis cannot find.

### Specific Spec Pressure Points

| Pressure Point | What the Equip Tool Tests |
|---------------|--------------------------|
| **Facet completeness** | If a consumer cannot "equip" a meaningful data category, the spec has a gap in its facet vocabulary. |
| **Encryption UX** | How do users manage encrypted vs. public facets visually? What does a "locked slot" mean in practice? Can the spec's encryption model be expressed through a visual metaphor? |
| **Pointer complexity** | What happens when a pointer breaks or goes stale? How does the UI represent a pointer to an offline resource? Does the spec provide enough metadata for a consumer to handle degraded pointers? |
| **Consent granularity** | Can users understand and manage per-facet consent through the equip interface? Is the `consents` array expressive enough for real consumer scenarios? |
| **Portaling** | Can a user "jump" to another world and see their equip carry over? Does the manifest contain everything the destination needs to reconstruct the equipped state? |
| **Facet versioning** | What happens when a facet schema changes between spec versions? Can the equip tool handle a manifest with mixed v0.1 and v0.2 facets? |
| **Manifest size** | How many equip slots can a user fill before hitting the 1 MB manifest limit? Does pointer-first design keep the manifest light enough? |
| **Signature lifecycle** | When a user modifies their equip (adds/removes a facet), the manifest must be re-signed. Is the re-signing flow fast enough for interactive use? |

---

## 6. Relationship to IWPS and Portaling

The Avatar Equip Tool directly connects to the portaling model described in the metaverse integration lane.

### Portaling as Equip Cargo

When a user "portals" — executing an IWPS Query + Teleport sequence — their equipped manifest is the cargo. The manifest carries:

- Who arrived (`subject`, `crossWorldProfile`)
- What they brought (equipped facets and pointers)
- What they allow (consent settings)
- What they can prove (compliance facets, claims)

### Destination World Behavior

The destination world reads the equip slots (facets) and renders what it supports:

1. **Supported equip items** render normally in the destination context.
2. **Unsupported equip items** gracefully degrade — shown as "incompatible" in the UI, per the UM spec's forward-compatibility rules.
3. **Consent-gated items** remain hidden unless the destination explicitly requests access and the manifest's consent settings permit it.
4. **Broken pointers** display a fallback state rather than failing the entire portal jump.

### Consumer-Visible IWPS Integration

The equip tool makes the IWPS + UM integration tangible for consumers:

- Before portaling: the user sees their full equip loadout.
- During portaling: the manifest travels as the portable document.
- After portaling: the destination world shows which equip items carried over, which degraded, and which were blocked by consent or incompatibility.

This is the consumer-visible manifestation of the technical portaling flow described in `integrations/metaverse.md` and `docs/explainers/metaverse-portaling.md`.

---

## 7. Technical Requirements

### Rendering
- 3D avatar rendering (Three.js, Babylon.js, or equivalent WebGL/WebGPU engine)
- GLB/glTF avatar model loading from pointer URLs
- Visual slot overlay system on the avatar model (highlight equip points)

### UM Specification Compliance
- UM manifest parser/generator conformant with v0.1 and v0.2 spec
- JSON-LD context handling (`schema.jsonld` for both versions)
- Structural validation against `schema.json`
- Conformance fixture validation (tool-generated manifests must pass the published conformance suite)

### Resolver Integration
- Publish manifests to `myum.net/{UMID}`
- Fetch and display existing manifests from the resolver
- UMID generation (`urn:uuid:<uuidv4>`)

### Equip Interface
- Drag-and-drop UI for equip management
- Category-based slot organization
- Real-time manifest preview (see the JSON-LD update as you equip)
- Undo/redo for equip actions

### Security and Privacy
- Ed25519 signing for v0.2 manifests (JCS canonicalization per RFC 8785)
- Per-facet encryption/decryption for private slots
- TTL management (issuedAt/expiresAt controls)
- Signature re-generation on manifest modification

### Export
- Export to valid JSON-LD (conformant with published UM schema)
- Export signed manifests (v0.2)
- Export unsigned manifests (v0.1, for draft/exploration use)

---

## 8. Open Questions

1. **Multi-avatar profiles:** Should the tool support multiple avatars for the same user, each with different equip configurations? (e.g., "work avatar" vs. "gaming avatar" vs. "public avatar")

2. **Encrypted facet visualization:** How should encrypted facets be visualized in the equip UI? Options include:
   - Locked slot icon (padlock overlay)
   - Blurred/frosted slot content
   - Vault metaphor (items stored in a sealed compartment)
   - Combination: visible category label, but blurred content until decrypted

3. **Wardrobe / saved configurations:** Should the tool include a "wardrobe" feature — saved equip configurations for different contexts? A user might have a "conference loadout" (professional profile, business credentials, payment handles) vs. a "gaming loadout" (avatar, inventory, social graph, gaming reputation).

4. **Sandbox integration:** How does the equip tool integrate with the interactive sandbox scenarios on `universalmanifest.net`? Could the sandbox scenarios drive equip tool tutorials?

5. **Offline-first behavior:** Given the UM spec's emphasis on local-first and constrained-device environments, should the equip tool work fully offline (editing a cached manifest) with sync-on-reconnect?

6. **Facet discovery:** How does a user discover new equip categories? Should the tool ship with a curated catalog of equip types, or should it dynamically discover available facet types from the UM registry (`spec/v0.1/REGISTRY.md`)?

7. **Multi-manifest management:** Should the tool manage a single manifest at a time, or support a manifest collection (multiple manifests for different subjects or contexts)?

---

## References

- UM Specification v0.1: `spec/v0.1/README.md`
- UM Specification v0.2: `spec/v0.2/README.md`
- Metaverse Integration Lane: `integrations/metaverse.md`
- Metaverse Portaling Explainer: `docs/explainers/metaverse-portaling.md`
- Envelope Topology Report: `docs/ENVELOPE-TOPOLOGY.md`
- UM Facet Registry: `spec/v0.1/REGISTRY.md`
- MUM Synchronization Profile: `docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
