# Universal Manifest -- Envelope Topology Report

This document settles the question: **What do we mean by "envelope" in Universal Manifest, and what is the structural topology of a manifest?**

It catalogs every usage of the term "envelope" across the repo, identifies inconsistencies, proposes a consistent terminology, and provides structural diagrams showing exactly how the pieces fit together.

---

## 1. Is a Universal Manifest ONE Envelope or MULTIPLE Envelopes?

**Answer: A Universal Manifest is ONE envelope. There is no nesting of envelopes.**

A manifest is a single, flat JSON-LD document with structured internal sections. Shards are not sub-envelopes. Pointers are not references to other envelopes. The signature does not create a wrapper envelope around the payload. There is exactly one document, one `@id`, one `subject`, one validity window, and (in v0.2) one signature.

### The correct mental model

A manifest is a **single container with labeled compartments**:

```
┌─────────────────────────────────────────────────┐
│  MANIFEST (one document, one @id)               │
│                                                 │
│  ┌───────────────────────────────────────────┐  │
│  │  HEADER                                   │  │
│  │  @context, @id, @type, manifestVersion    │  │
│  │  subject, issuedAt, expiresAt             │  │
│  └───────────────────────────────────────────┘  │
│                                                 │
│  ┌───────────────────────────────────────────┐  │
│  │  PAYLOAD SECTIONS (all optional)          │  │
│  │                                           │  │
│  │  shards[]    ← composable data slots      │  │
│  │  claims[]    ← assertions about subject   │  │
│  │  consents[]  ← privacy/disclosure rules   │  │
│  │  devices[]   ← registered endpoints       │  │
│  │  pointers[]  ← URLs to external data      │  │
│  └───────────────────────────────────────────┘  │
│                                                 │
│  ┌───────────────────────────────────────────┐  │
│  │  SIGNATURE (optional v0.1, required v0.2) │  │
│  │  algorithm, canonicalization, keyRef,      │  │
│  │  publicKeySpkiB64, value                  │  │
│  └───────────────────────────────────────────┘  │
│                                                 │
└─────────────────────────────────────────────────┘
```

There is no wrapping. The signature sits alongside the payload sections as a sibling property, not around them. During verification, the signature property is temporarily removed to compute the canonical signing input, but structurally it is a peer property.

### What a manifest is NOT

- NOT a nested set of envelopes (no envelope-within-envelope)
- NOT an outer envelope wrapping an inner document
- NOT a signature wrapper around a payload envelope
- NOT a container of sub-containers that are each independently addressable

---

## 2. How "Envelope" Is Currently Used in the Repo

### 2.1 Complete usage catalog

The word "envelope" appears in the codebase in **five distinct senses**. Here is the full catalog, organized by meaning:

#### Sense A: "The whole manifest is an envelope" (manifest = envelope)

This is the most common usage. The word "envelope" is used as a synonym for "manifest" or "document format," meaning the standardized container that carries payload data.

| File | Line/Context | Exact phrasing |
|------|-------------|----------------|
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 21 | "UM is the standard envelope for portable identity, state, and capability across any system boundary" |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 300 | "the standard envelope adapts to a radically different domain" |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 514 | "Envelope, not database" |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 532 | "a standard envelope for identity, claims, consents..." |
| `packages/universal-manifest/src/index.ts` | line 76 | "The manifest is the top-level envelope that binds a subject identity to a set of shards..." |
| `docs/STATE-OF-THE-PROJECT.md` | line 265 | "treat the manifest as an envelope that drives projections" |
| `docs/journeys/commercial/enterprise-journey.md` | line 17 | "The manifest envelope is the same whether it describes an artist, a venue, or a display device" |
| `docs/journeys/commercial/enterprise-journey.md` | line 51 | "the manifest envelope (@context, @id, @type...) is identical across all entity types" |
| `integrations/social.md` | line 57 | "the signable envelope that carries cross-surface claims/consents" |
| `integrations/oma-trust.md` | line 23 | "keeping the core UM envelope stable" |
| `integrations/rp1-spatial-fabric.md` | line 21 | "the portable envelope for subject identity, consent, and pointer routing" |
| `docs/journeys/README.md` | line 67 | "the same core manifest envelope" |
| `docs/DECISIONS.md` | line 291 | "composable envelope over monolith" |
| `docs/design/ANIMATION-PLACEMENT-PLAN.md` | line 13 | "UM core envelope" |
| `docs/design/ANIMATION-PLACEMENT-PLAN.md` | line 21 | "one shared UM envelope" |
| `docs/reports/2026-02-22-first-time-reader-human-gate-checklist.md` | line 26 | "shared envelope across systems" |
| `docs/reports/2026-02-23-first-time-reader-test-results-human.md` | line 62 | "a versioned JSON-LD manifest/envelope" |
| `site/src/content/docs/getting-started/universal-manifest-overview.md` | line 30 | "Think of it as an envelope: the outside is always the same shape, but the contents vary" |

#### Sense B: "The signature field is an envelope" (signature = envelope)

The `signature` property is frequently called a "signature envelope," meaning the JSON object that wraps the cryptographic signature value and its metadata.

| File | Line/Context | Exact phrasing |
|------|-------------|----------------|
| `spec/v0.1/README.md` | line 27 | "signature envelope for integrity" |
| `spec/v0.1/schema.json` | line 55 | "Permissive v0.1 signature envelope" |
| `spec/v0.1/CONFORMANCE.md` | line 86 | "signature only as a permissive envelope" |
| `spec/v0.2/SIGNATURE-PROFILE.md` | line 76 | "Signature envelope shape (draft)" |
| `spec/v0.2/CONFORMANCE.md` | line 52 | "Embed the signature envelope" |
| `spec/v0.2/CONFORMANCE.md` | line 85 | "signature envelope misuse" |
| `packages/universal-manifest/src/index.ts` | line 44 | "Signature envelope for v0.1 manifests" |
| `packages/universal-manifest/src/index.ts` | line 57 | "Signature envelope for v0.2 manifests" |
| `packages/universal-manifest/README.md` | line 42-43 | "Loosely-typed signature envelope for v0.1" / "Ed25519 + JCS signature envelope for v0.2" |
| `docs/DECISIONS.md` | line 23 | "permissive placeholder envelope" |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 52 | "Cryptographic integrity envelope" |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 85 | "v0.1 is a permissive envelope" |
| `docs/UNIVERSAL-MANIFEST-BRIEFING.md` | line 100 | "Attach the signature envelope back to the manifest" |
| `docs/DEPTH-AND-SCOPE.md` | line 27 | "signature envelope + short TTL" |
| `docs/DEPTH-AND-SCOPE.md` | line 46 | "permissive signature envelope" |
| `docs/DEPTH-AND-SCOPE.md` | line 184 | "first real signing envelope" |
| `docs/STUB-MANIFESTS.md` | line 53 | "Integrity envelope (format intentionally permissive)" |
| `integrations/reference-runtime.md` | line 69 | "signature is optional (permissive envelope)" |
| `docs/journeys/commercial/app-developer-journey.md` | line 55 | "publicKeySpkiB64 from the signature envelope" |
| `docs/DONE-DONE-DEFINITION.md` | line 123 | "integrity envelope behavior" |
| `docs/reports/2026-02-12-spec-status-and-foundations-audit.md` | line 23 | "Integrity envelope semantics by profile" |

#### Sense C: "A shard or fixture called 'envelope'" (envelope as a name)

Some fixtures and shard names use "envelope" as a descriptive label.

| File | Line/Context | Exact phrasing |
|------|-------------|----------------|
| `spec/v0.1/REGISTRY.md` | line 19 | "venuePolicy -- Venue policy envelope" |
| `examples/v0.1/stubs/display-envelope-manifest.jsonld` | filename | "display-envelope-manifest" |
| `docs/STUB-MANIFESTS.md` | line 26 | "display-envelope-manifest.jsonld" |
| `docs/STUB-MANIFESTS.md` | line 199 | "the policy envelope" |
| `docs/STUB-MANIFESTS.md` | line 671 | "minimal display-local capsule" |

#### Sense D: "Envelope as visual/iconic metaphor" (teaching scripts)

The teaching scripts considered a "sealed envelope" as one candidate icon and use "envelope" when discussing the manifest's structural layers visually.

| File | Line/Context | Exact phrasing |
|------|-------------|----------------|
| `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md` | line 62 | "Concept 2: The Sealed Envelope with Wax Seal" |
| `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md` | line 75-87 | Full description of envelope icon concept |
| `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md` | line 252 | "The outermost is the envelope, the middle is the integrity layer" |
| `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md` | line 341 | "The outer shape is the envelope; the inner shape is the data" |
| `docs/teaching-scripts/03-SCRIPT-IDEAS.md` | line 27 | "The viewer learns the word 'envelope' without needing to know JSON-LD" |
| `docs/teaching-scripts/02-SCRIPT-FORMAT.md` | line 36, 74, 154 | "manifest-envelope" as a teaching concept tag |

#### Sense E: "Envelope as a protocol/cryptographic wrapper" (external/future)

References to JWE envelopes or external attestation envelopes from other standards.

| File | Line/Context | Exact phrasing |
|------|-------------|----------------|
| `docs/security/THREAT-MODEL.md` | line 265 | "JWE envelopes" |
| `docs/reports/2026-02-22-omatrust-integration-assessment.md` | line 123 | "OMATrust attestation envelopes/proofs" |

### 2.2 Inconsistencies identified

The repo uses "envelope" in two fundamentally different ways that create confusion:

1. **Sense A** says "the manifest IS an envelope" -- meaning the entire document is the container.
2. **Sense B** says "the signature IS an envelope" -- meaning the `signature` JSON object wraps the cryptographic value.

These two usages are incompatible if read literally. The manifest cannot be "an envelope" while simultaneously containing a sub-object that is also called "an envelope." This is the core terminology ambiguity.

Additional inconsistency: the briefing document says "Envelope, not database" (Sense A) and three lines later refers to "Cryptographic integrity envelope" (Sense B) in the same table. A reader encounters both senses within seconds.

### 2.3 Where "envelope" should be replaced

The onboarding language audit (`docs/reports/2026-02-23-wo-0039-onboarding-language-source-map-and-rewrite-plan.md`) already flagged this problem. It found that "envelope" appears on first-read pages without definition and recommended replacing it with "container" or "a standard document wrapper with fixed header fields."

---

## 3. The Topology of a Universal Manifest

### 3.1 Structural layers

A Universal Manifest has **three conceptual layers**, but they are not nested containers. They are regions within a single flat JSON object:

```
LAYER 1: HEADER (required fields)
  @context           → vocabulary reference
  @id                → globally unique manifest ID (UMID)
  @type              → "um:Manifest"
  manifestVersion    → "0.1" or "0.2"
  subject            → who/what this manifest is about
  issuedAt           → when it was created
  expiresAt          → when it expires

LAYER 2: PAYLOAD (optional structured sections)
  shards[]           → named data compartments
  claims[]           → assertions about the subject
  consents[]         → disclosure/privacy controls
  devices[]          → registered endpoints
  pointers[]         → URLs to external authoritative data

LAYER 3: INTEGRITY (optional in v0.1, required in v0.2)
  signature {}       → cryptographic proof of authenticity
    .algorithm       → "Ed25519"
    .canonicalization → "JCS-RFC8785"
    .keyRef          → where to find the public key
    .publicKeySpkiB64 → inline public key (optional)
    .value           → the signature bytes
    .statusRef       → revocation endpoint (optional)
    .revocationCursor → revocation cursor (optional)
```

These layers are conceptual groupings. In the actual JSON, all three layers are **sibling properties** at the top level of a single object.

### 3.2 How shards relate to the manifest

Shards are **compartments within the single manifest**, not sub-envelopes. Each shard is a named JSON object in the `shards[]` array.

```
manifest
  └── shards[]
       ├── shard: "publicProfile"
       │     ├── @type: "um:Shard"
       │     ├── name: "publicProfile"
       │     └── entity: { @id, @type, name, ... }
       │
       ├── shard: "deviceRegistration"
       │     ├── @type: "um:Shard"
       │     ├── name: "deviceRegistration"
       │     ├── ref: "https://..." (canonical source)
       │     └── entity: { @id, @type, ... }
       │
       └── shard: "crossWorldProfile"
             ├── @type: "um:Shard"
             ├── name: "crossWorldProfile"
             └── entity: { displayName, homeWorld, ... }
```

Key properties of shards:

- Shards do NOT have their own signatures. They are covered by the manifest-level signature.
- Shards do NOT have their own validity windows. They inherit `issuedAt`/`expiresAt` from the manifest.
- Shards do NOT have their own `@id` at the manifest level (though they may carry one for internal entity identification).
- Shards CAN embed data (`entity`) or reference external data (`ref`), or both.
- Shards are NOT independently addressable or resolvable. You resolve the manifest, then read the shards you understand.

**Shards are best described as: named data slots within a single manifest.**

### 3.3 How pointers relate to the manifest

Pointers are **outbound references from the manifest to external data sources**. They are not sub-envelopes, not links to other manifests (though they could be), and not part of the manifest's own payload.

```
manifest
  └── pointers[]
       ├── { rel: "canonical", href: "https://pod.example/profile.jsonld" }
       ├── { rel: "portfolio", href: "https://portfolio.example/works" }
       └── { rel: "social",    href: "https://social.example/users/bob" }
```

Key properties of pointers:

- Pointers are URLs. The manifest does NOT embed the data they point to.
- Pointers are covered by the manifest signature (if you change a pointer URL, the signature breaks).
- Following a pointer is the consumer's choice. A consumer that does not understand a pointer's `rel` ignores it.
- Pointers do NOT make the manifest depend on the target being available. The manifest is valid even if a pointer target is offline.

**Pointers are best described as: annotated links to external authoritative data.**

### 3.4 How the signature covers the structure

The signature does not "wrap" the manifest. It is a sibling property that covers everything else through a sign-then-attach pattern.

#### Signing process (what the signature covers)

```
  START: complete manifest JSON object
    │
    ▼
  STEP 1: Remove the "signature" property entirely
    │
    ▼
  STEP 2: Canonicalize remaining JSON via JCS (RFC 8785)
    │         → produces deterministic UTF-8 bytes
    ▼
  STEP 3: Sign the canonical bytes with Ed25519
    │
    ▼
  STEP 4: Attach signature object back to manifest
    │
    ▼
  RESULT: signed manifest (original content + signature property)
```

#### What this means for coverage

The signature covers **everything except itself**:

```
┌─────────────────────────────────────────┐
│                                         │
│  ┌──── SIGNED (canonicalized) ───────┐  │
│  │                                   │  │
│  │  @context ✓                       │  │
│  │  @id ✓                            │  │
│  │  @type ✓                          │  │
│  │  manifestVersion ✓                │  │
│  │  subject ✓                        │  │
│  │  issuedAt ✓                       │  │
│  │  expiresAt ✓                      │  │
│  │  shards[] ✓  (all shard content)  │  │
│  │  claims[] ✓                       │  │
│  │  consents[] ✓                     │  │
│  │  devices[] ✓                      │  │
│  │  pointers[] ✓                     │  │
│  │                                   │  │
│  └───────────────────────────────────┘  │
│                                         │
│  ┌──── NOT SIGNED ───────────────────┐  │
│  │  signature {}  (excluded from     │  │
│  │    signing input to avoid         │  │
│  │    circularity)                   │  │
│  └───────────────────────────────────┘  │
│                                         │
└─────────────────────────────────────────┘
```

The signature is NOT a wrapping layer. It is a **detached proof** that sits alongside the content it proves. This is structurally similar to how JWS detached signatures work, not how PKCS#7/CMS wrapping works.

### 3.5 How v0.2 changes the structure compared to v0.1

The JSON structure is nearly identical between v0.1 and v0.2. The changes are:

| Aspect | v0.1 | v0.2 |
|--------|------|------|
| `signature` required? | No | Yes |
| `signature.algorithm` | Any (permissive) | Must be `"Ed25519"` |
| `signature.canonicalization` | Not specified | Must be `"JCS-RFC8785"` |
| `signature.value` | Informational | Verified cryptographically |
| `signature.publicKeySpkiB64` | Not defined | Optional (for offline verification) |
| `signature.statusRef` | Not defined | Optional (revocation endpoint) |
| `signature.revocationCursor` | Not defined | Optional (revocation cursor) |
| `manifestVersion` | `"0.1"` | `"0.2"` |

The **shape** does not change. The **semantics** of the signature change from "informational placeholder" to "cryptographically verified proof." The topology is the same.

---

## 4. Visual Topology Maps

### 4.1 v0.1 Manifest Topology (minimal)

```
┌─────────────────────────────────────────────┐
│  um:Manifest  (v0.1)                        │
│                                             │
│  @context ─── vocabulary reference          │
│  @id ──────── "urn:uuid:..." (UMID)         │
│  @type ─────── "um:Manifest"                │
│  manifestVersion ── "0.1"                   │
│  subject ──── "did:key:z6Mk..."             │
│  issuedAt ─── "2026-02-11T20:45:58Z"        │
│  expiresAt ── "2026-02-12T20:45:58Z"        │
│                                             │
│  shards: []  (empty)                        │
│                                             │
└─────────────────────────────────────────────┘
```

### 4.2 v0.1 Manifest Topology (with shards and signature)

```
┌──────────────────────────────────────────────────────┐
│  um:Manifest  (v0.1)                                 │
│                                                      │
│  HEADER                                              │
│  ├── @context, @id, @type, manifestVersion           │
│  ├── subject: "did:web:venue.localartist.network"    │
│  ├── issuedAt / expiresAt                            │
│                                                      │
│  SHARDS                                              │
│  ├── ┌──────────────────────────────────────┐        │
│  │   │ um:Shard "canonicalProfilePointer"   │        │
│  │   │   ref: https://pod.example/profile   │───────────► external
│  │   │   entity: { @id, @type, name }       │        │    data
│  │   └──────────────────────────────────────┘        │
│  │                                                   │
│  └── ┌──────────────────────────────────────┐        │
│      │ um:Shard "deviceRegistration"        │        │
│      │   entity: { @id, @type, name, desc } │        │
│      └──────────────────────────────────────┘        │
│                                                      │
│  SIGNATURE (informational only in v0.1)              │
│  ├── algorithm: "Ed25519"                            │
│  ├── keyRef: "did:web:...#keys-1"                    │
│  └── value: "BASE64URL_SIGNATURE_PLACEHOLDER"        │
│                                                      │
└──────────────────────────────────────────────────────┘
```

### 4.3 v0.2 Signed Manifest Topology (with shards)

```
┌────────────────────────────────────────────────────────────┐
│  um:Manifest  (v0.2)                                       │
│                                                            │
│  ┌──── SIGNING INPUT (everything below) ────────────────┐  │
│  │                                                      │  │
│  │  HEADER                                              │  │
│  │  ├── @context: ".../v0.2/schema.jsonld"              │  │
│  │  ├── @id: "urn:uuid:44444444-..."                    │  │
│  │  ├── @type: "um:Manifest"                            │  │
│  │  ├── manifestVersion: "0.2"                          │  │
│  │  ├── subject: "did:example:venue-edge"               │  │
│  │  ├── issuedAt: "2026-02-27T00:00:00.000Z"           │  │
│  │  └── expiresAt: "2026-02-28T00:00:00.000Z"          │  │
│  │                                                      │  │
│  │  SHARDS                                              │  │
│  │  ├── ┌──────────────────────────────────┐            │  │
│  │  │   │ um:Shard "venueProfile"          │            │  │
│  │  │   │   entity: schema:Place           │            │  │
│  │  │   │   { name, description }          │            │  │
│  │  │   └──────────────────────────────────┘            │  │
│  │  │                                                   │  │
│  │  └── ┌──────────────────────────────────┐            │  │
│  │      │ um:Shard "deviceRegistration"    │            │  │
│  │      │   ref: https://pod.example/...   │────────────────► external
│  │      │   entity: { @id, @type, ... }    │            │  │
│  │      └──────────────────────────────────┘            │  │
│  │                                                      │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                            │
│  SIGNATURE (cryptographically verified)                    │
│  ├── algorithm: "Ed25519"                                  │
│  ├── canonicalization: "JCS-RFC8785"                        │
│  ├── keyRef: "did:example:venue-edge#key-1"                │
│  ├── created: "2026-02-27T00:00:00.000Z"                   │
│  ├── publicKeySpkiB64: "MCowBQY..."                        │
│  └── value: "NkTRGYGG7jEL..."                              │
│                                                            │
└────────────────────────────────────────────────────────────┘
```

### 4.4 v0.2 Manifest with Pointers

```
┌───────────────────────────────────────────────────┐
│  um:Manifest  (v0.2)                              │
│                                                   │
│  HEADER                                           │
│  ├── @id, @type, manifestVersion, subject         │
│  ├── issuedAt / expiresAt                         │
│                                                   │
│  POINTERS                                         │
│  ├── { rel: "canonical",                          │
│  │     href: "https://pod.example/profile" } ─────────► Pod profile
│  │                                                │
│  ├── { rel: "portfolio",                          │
│  │     href: "https://portfolio.example/works" } ─────► Portfolio site
│  │                                                │
│  └── { rel: "social",                             │
│        href: "https://social.example/users/bob" } ────► Social profile
│                                                   │
│  SIGNATURE                                        │
│  ├── algorithm, canonicalization                  │
│  ├── keyRef, publicKeySpkiB64                     │
│  └── value                                        │
│                                                   │
└───────────────────────────────────────────────────┘

Pointer targets live OUTSIDE the manifest.
The manifest REFERENCES them; it does not CONTAIN them.
Pointer URLs are signed (changing them breaks the signature).
Pointer targets are NOT signed (they are external documents).
```

### 4.5 Signature Coverage Map

```
              ┌──────────────────────────────┐
              │     MANIFEST JSON OBJECT     │
              │                              │
   SIGNED     │  @context        ✓ signed    │
   ┌──────────│  @id             ✓ signed    │
   │          │  @type           ✓ signed    │
   │          │  manifestVersion ✓ signed    │
   │          │  subject         ✓ signed    │
   │  JCS     │  issuedAt        ✓ signed    │
   │  canon-  │  expiresAt       ✓ signed    │
   │  icalize │  shards[...]     ✓ signed    │
   │  ────►   │  claims[...]     ✓ signed    │
   │  Ed25519 │  consents[...]   ✓ signed    │
   │  sign    │  devices[...]    ✓ signed    │
   │          │  pointers[...]   ✓ signed    │
   └──────────│                              │
              │  signature {     ✗ excluded  │
              │    algorithm     ✗           │
              │    value         ✗           │
              │    ...           ✗           │
              │  }                           │
              │                              │
              └──────────────────────────────┘
```

### 4.6 Full Topology: Rich Manifest with All Sections

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│  um:Manifest  v0.2                                               │
│  @id: urn:uuid:7b8c9d0e-...                                     │
│  subject: did:example:metaverse-user-01                          │
│  issuedAt ─────────────────────── expiresAt                      │
│  │         validity window         │                             │
│  ├─────────────────────────────────┤                             │
│                                                                  │
│  ┌── CLAIMS ──────────────────────────────────────────────────┐  │
│  │  { name: "metaverse.role", value: "creator" }              │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌── CONSENTS ────────────────────────────────────────────────┐  │
│  │  { name: "metaverse.profilePublic", value: "allowed" }     │  │
│  │  { name: "metaverse.socialGraphShare", value: "restricted" │  │
│  │  { name: "metaverse.voiceCapture", value: "denied" }       │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌── POINTERS (references to external data) ──────────────────┐  │
│  │  metaverse.profile  ──────────────────────────► external    │  │
│  │  metaverse.avatar   ──────────────────────────► external    │  │
│  │  metaverse.inventory ─────────────────────────► external    │  │
│  │  metaverse.socialGraph ───────────────────────► external    │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌── SHARDS (embedded data compartments) ─────────────────────┐  │
│  │  ┌─────────────────────────────────────────────────┐       │  │
│  │  │ um:Shard "crossWorldProfile"                    │       │  │
│  │  │   entity:                                       │       │  │
│  │  │     displayName: "Nova"                         │       │  │
│  │  │     homeWorld: "world://origin.example/home"    │       │  │
│  │  │     supportedWorlds: [...]                      │       │  │
│  │  └─────────────────────────────────────────────────┘       │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌── SIGNATURE ───────────────────────────────────────────────┐  │
│  │  Ed25519 / JCS-RFC8785                                     │  │
│  │  keyRef: did:example:metaverse-user-01#key-1               │  │
│  │  value: <base64url Ed25519 signature>                      │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

### 4.7 Manifests in a Network (how manifests relate to each other)

Manifests are independent documents. They do NOT nest inside each other. They MAY reference each other through pointers or through shared `subject` identifiers.

```
  ┌─────────────────────┐      ┌─────────────────────┐
  │ Manifest A          │      │ Manifest B          │
  │ subject: did:a      │      │ subject: did:b      │
  │                     │      │                     │
  │ pointer ────────────────►  │                     │
  │   (href to B's @id) │      │                     │
  │                     │      │                     │
  │ shard: "profile"    │      │ shard: "venue"      │
  │ shard: "prefs"      │      │ shard: "devices"    │
  │ signature ✓         │      │ signature ✓         │
  └─────────────────────┘      └─────────────────────┘
        │                             │
        │                             │
        ▼                             ▼
  Independent documents.     Independent documents.
  Each has its own @id,      Each signed separately.
  own subject, own TTL,      No nesting.
  own signature.             No parent-child.
```

---

## 5. Recommended Terminology

### 5.1 Should we use "envelope" at all?

**Recommendation: Phase out "envelope" for the manifest. Keep it only for the signature field, with a qualifier.**

The word "envelope" causes three problems:

1. **Overloaded**: It is used to mean both "the whole manifest" (Sense A) and "the signature field" (Sense B) within the same documents.
2. **Suggests nesting**: "Envelope" naturally implies something that wraps around something else, creating an inside/outside relationship. But the signature does not wrap the manifest -- it sits alongside it. And the manifest itself is not wrapped in anything.
3. **Collision with email**: As the teaching-scripts evaluation noted (01-ICONIC-REPRESENTATION.md, line 87), "envelope" is strongly associated with email, which creates confusion.

### 5.2 Proposed terminology guide

| Concept | Recommended Term | Definition | When to use | When NOT to use |
|---------|-----------------|------------|-------------|-----------------|
| The whole manifest document | **manifest** | A single JSON-LD document that carries identity, state, and capability data for a subject | Always when referring to the complete document | Do not call it "envelope" or "capsule" without qualification |
| The document format/shape | **format** or **document format** | The standardized JSON-LD structure that all manifests share | When discussing the spec's structural contract | Do not call it "envelope format" |
| The manifest as a portable unit | **portable document** or **state document** | A manifest when emphasizing its transport-between-systems property | When explaining portability to newcomers | Do not use "state capsule" without defining it first |
| The `signature` field | **signature block** | The JSON object containing the cryptographic signature, algorithm, key reference, and verification metadata | When referring to the `signature` property in the JSON | Do not call it "signature envelope" (it is not wrapping anything) |
| The signature's signing scope | **signing input** | The manifest JSON with the `signature` property removed, then JCS-canonicalized | When describing what gets signed | Do not call it "the envelope contents" |
| A shard | **shard** or **data slot** | A named compartment within the manifest's `shards` array that carries domain-specific data | When referring to items in `shards[]` | Do not call shards "sub-envelopes" or "inner envelopes" |
| A pointer | **pointer** or **data reference** | A URL in the `pointers` array that links to an external authoritative data source | When referring to items in `pointers[]` | Do not call pointers "external envelopes" |
| The header fields | **header** or **required fields** | The fixed set of required properties: `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt` | When discussing the structural skeleton | Do not call it "the outer envelope" |
| The payload sections | **payload sections** or **content sections** | The optional arrays: `shards`, `claims`, `consents`, `devices`, `pointers` | When discussing the variable content of a manifest | Do not call it "the inner envelope" |
| The manifest as a whole concept | **Universal Manifest** or **UM** | The specification, the format, and the ecosystem | When referring to the project/standard | Do not use "envelope standard" |

### 5.3 Migration from current terms

| Current term (to retire or qualify) | Replacement |
|-------------------------------------|-------------|
| "envelope" (when meaning the whole manifest) | **manifest** or **document** |
| "standard envelope" | **standard format** or **shared document format** |
| "portable envelope" | **portable document** |
| "composable envelope" | **composable manifest** |
| "envelope contract" | **document format contract** or **manifest contract** |
| "signature envelope" | **signature block** |
| "permissive envelope" (re: v0.1 signature) | **permissive signature** or **placeholder signature** |
| "integrity envelope" | **integrity layer** or **signature profile** |
| "state capsule" (when used without definition) | **portable state document** (or define "state capsule" explicitly on first use) |

### 5.4 When "envelope" is still acceptable

There are two contexts where "envelope" remains acceptable:

1. **Analogy/metaphor in teaching contexts**: "Think of a manifest like an envelope with a fixed-format address block on the outside and variable contents inside." This is fine as long as it is clearly an analogy, not a technical term.

2. **External protocol references**: "JWE envelopes" or "OMATrust attestation envelopes" refer to other standards' concepts and should not be renamed.

---

## 6. How This Relates to the Capsule-Pod Icon

The teaching-scripts system (docs/teaching-scripts/01-ICONIC-REPRESENTATION.md) chose the **Capsule-Pod** as the iconic visual character for Universal Manifest. This section maps the pod metaphor to the actual topology.

### 6.1 The Capsule-Pod shape

```
      ╭────────╮
     ╱  ╭────╮  ╲
    │   │ UM │   │       Outer shell = manifest boundary
     ╲  ╰────╯  ╱        Gap = integrity/signature layer
      ╰────────╯         Inner payload = content sections
```

The pod has three visual elements:

1. **Outer shell**: The manifest's structural boundary (header + format contract)
2. **Gap between shell and payload**: The integrity layer (signature verification)
3. **Inner payload**: The content sections (shards, claims, consents, devices, pointers)

### 6.2 How the pod maps to the topology

| Pod visual element | Topology equivalent | Notes |
|-------------------|---------------------|-------|
| Outer shell | The manifest document itself, especially the required header fields | The shell defines the shape. All manifests have the same outer shape regardless of content. |
| Gap / space between shell and payload | The signature block and verification process | The gap "lights up" during verification. Green = valid signature. Red = tampered. This is the most powerful visual metaphor in the system. |
| Inner payload | The payload sections (shards, claims, consents, devices, pointers) | The contents vary by use case but always sit inside the same shell. |
| Pod opening (projection) | Consumer reading specific shards/sections | The shell peels open, contents emerge toward their consumer destinations. |
| Pod traveling | The manifest being transported between systems | The pod moves as a unit -- there are no sub-pods traveling separately. |

### 6.3 What the pod represents

**The pod represents the entire manifest -- not just the payload, not just the wrapper.**

The pod is a single object that travels as a unit. It is not an envelope that you open and discard. The shell and the payload are one thing. This is the correct metaphor: the manifest is a self-contained unit where the structure (header + signature) and the content (shards + claims + consents + devices + pointers) travel together inseparably.

The pod metaphor is better than the envelope metaphor because:

- An envelope is something you **open and throw away**. A manifest is something you **verify and keep intact**.
- An envelope has contents that can be **removed from the envelope**. A manifest's shards cannot be separated from the manifest's signature -- removing a shard invalidates the signature.
- An envelope is **passive packaging**. A pod is **active protection** (the gap = integrity layer) around active payload.

### 6.4 Where the pod metaphor gets tricky

The pod metaphor breaks down slightly in one area: **projection**. When a consumer reads specific shards from a manifest, the teaching scripts show the pod "opening up" and shards floating toward consumers. This could imply that shards leave the pod, but in reality the manifest stays intact and the consumer simply reads the parts it understands. The teaching scripts handle this correctly by showing the inner payload remaining visible as the source while shard elements float toward destinations.

---

## 7. Summary of Findings

### One envelope or multiple?
One. A Universal Manifest is a single flat JSON-LD document with structured internal sections. No nesting.

### Current terminology problem
"Envelope" is used ambiguously for both the whole manifest and the signature field. This confuses readers.

### Structural topology
Three conceptual layers (header, payload sections, signature) that are all sibling properties in a single JSON object. The signature does not wrap the content; it sits alongside it as a detached proof.

### Recommended change
Phase out "envelope" for the manifest. Use "manifest" or "document." Rename "signature envelope" to "signature block." Keep "envelope" only for teaching analogies and external protocol references.

### Capsule-Pod alignment
The pod correctly represents the manifest as a single self-contained unit with structural boundary (shell), integrity layer (gap), and payload (inner rectangle). The pod metaphor is more accurate than the envelope metaphor.

---

## Appendix: Decision Record

This report was produced on 2026-02-27 by analyzing:

- All spec artifacts (v0.1 and v0.2 schemas, contexts, conformance, signature profile)
- All example manifests (v0.1 and v0.2, including shards, pointers, revocation metadata)
- The TypeScript helper package (types and validation logic)
- The reference runtime integration contract
- The teaching-scripts visual design system
- Every usage of the word "envelope" across the entire repository (189+ matches)
- Every usage of the word "capsule" across the repository
- The onboarding language audit and rewrite plan
- The project decisions log

Files contributing to this analysis:

- `spec/v0.1/README.md`
- `spec/v0.1/schema.json`
- `spec/v0.1/schema.jsonld`
- `spec/v0.2/README.md`
- `spec/v0.2/schema.json`
- `spec/v0.2/SIGNATURE-PROFILE.md`
- `packages/universal-manifest/src/index.ts`
- `examples/v0.1/minimal-manifest.jsonld`
- `examples/v0.1/manifest-with-shards.jsonld`
- `examples/v0.2/minimal-signed-manifest.jsonld`
- `examples/v0.2/manifest-with-shards-signed.jsonld`
- `examples/v0.2/manifest-with-pointers-signed.jsonld`
- `examples/v0.2/manifest-with-revocation-metadata.jsonld`
- `integrations/reference-runtime.md`
- `docs/DECISIONS.md`
- `docs/UNIVERSAL-MANIFEST-BRIEFING.md`
- `docs/teaching-scripts/01-ICONIC-REPRESENTATION.md`
- `docs/reports/2026-02-23-wo-0039-onboarding-language-source-map-and-rewrite-plan.md`
