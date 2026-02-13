# Universal Manifest — Depths & Scope (High Level)

This document maps the **breadth (scope)** and **depth (layers)** of the Universal Manifest project so we can:

- avoid accidental “overbuild”
- keep v0.1 adoptable by multiple systems (LAN, future social/profile, third parties)
- clearly separate **normative spec** from **examples**, **integrations**, and **research**

If you only read one thing first:

- `docs/PROJECT-VISION.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DONE-DONE-DEFINITION.md`

---

## 1) What this project is

The **Universal Manifest** is a **portable state capsule**: a single document that can be transferred between compatible apps/devices/services to convey:

- **who** the subject is (identity references)
- **what** the subject can do (claims / roles / permissions)
- **what’s allowed** to be shown/shared (consents)
- **what devices** are in scope (devices + trust levels)
- **where canonical data lives** (pointers)
- **how it composes** (shards)
- **how integrity is asserted** (signature envelope + short TTL)

This is a **spec repo**, not an application.

---

## 2) Core constraints (the “shape” we must preserve)

These constraints appear repeatedly across the vision + research:

1. **Local-first reality**
   - Public displays and venue edges must tolerate partial connectivity.
2. **Small, cacheable capsule**
   - Consumers cache full manifests only while “in use”, and log mostly by manifest ID.
3. **No forced identity method**
   - DIDs are recommended but not mandatory; `subject` is any stable URI.
4. **Patches over payloads**
   - Prefer `pointers` + small `shards` over embedding large data blobs.
5. **Security as an incremental profile**
   - v0.1 has a permissive signature envelope; canonical signing format is a later milestone.

Primary references:

- `docs/PROJECT-VISION.md`
- `docs/CRUCIAL-DETAILS.md`
- `docs/DECISIONS.md`
- `spec/v0.1/README.md`

---

## 3) Depth map (layers of the repo)

Think of this repo as layers from “most normative” to “most contextual”.

### Layer A — Normative spec (`spec/`)

**Goal:** define the stable v0.1 contract:

- JSON-LD context and base semantics (`spec/v0.1/schema.jsonld`)
- structural schema (`spec/v0.1/schema.json`)
- overview and constraints (`spec/v0.1/README.md`)

Non-normative guidance adjacent to spec:

- well-known names registry (`spec/v0.1/REGISTRY.md`)
- conformance requirements + fixture list (`spec/v0.1/CONFORMANCE.md`)

### Layer B — Fixtures (`examples/`)

**Goal:** “show, don’t tell”:

- minimal valid examples
- richer near-real stubs used to drive integrations and validate tooling
- invalid fixtures to test failure modes (conformance)

Index:

- `docs/STUB-MANIFESTS.md`

### Layer C — Integrations (`integrations/`)

**Goal:** adoption recipes for concrete surfaces (without changing the core contract):

- LAN edge/display/admin and Shield storage/transport (`integrations/lan.md`)
- Social/profile surfaces and interoperability pointers (`integrations/social.md`)

### Layer D — Tooling (`packages/`)

**Goal:** help producers/consumers adopt the spec quickly:

- lightweight TypeScript types + runtime assertion for v0.1 (`packages/universal-manifest/`)
- fixture validation script run via `npm test`

This layer should stay small and “reference quality”, not become a framework.

### Layer E — Research (background) (`research/`)

**Goal:** preserve the design-library context that motivates the spec.

- imported docs are **not normative**
- they drive decisions, but spec changes must be recorded in `docs/DECISIONS.md`

Index:

- `research/README.md`

---

## 4) Scope map (what’s in-scope vs out-of-scope)

### In scope (v0.1 and near-term)

- A stable **document shape** (`lan:Manifest`) and composition primitive (`lan:Shard`)
- A minimal set of sections: `claims`, `consents`, `devices`, `pointers`, `signature` (permissive)
- Guidance for caching, TTL, and logging by `@id`
- Examples + stubs that exercise realistic scenarios:
  - venue/edge identity + policy
  - device enrollment + trust
  - creator public capsule
  - social/profile projection via a shard (`schema:Person`)

### Explicitly out of scope (v0.1)

- A mandated DID method/provider
- A full crypto suite implementation
- A single “canonical profile schema” for all entities
- Embedding large media payloads
- Full revocation registry + recovery workflows (kept as future work)

See:

- `docs/PROJECT-VISION.md` (non-goals)
- `docs/DECISIONS.md` (security scope)

---

## 5) Adoption model (how other systems adopt this)

Not every adopter needs the same depth. Design for adoption tiers:

1. **Tier 0 — Parse-only**
   - validate `@type`, TTL, and treat unknown fields as opaque
2. **Tier 1 — Pointers consumer**
   - use `pointers` to fetch canonical content (Pod, ActivityPub, etc.)
3. **Tier 2 — Projection renderer**
   - render known `shards` (e.g., `publicProfile`, `publicCapsule`)
4. **Tier 3 — Verified consumer**
   - enforce signature verification + TTL; reject on failure
5. **Tier 4 — Issuer**
   - produce signed manifests, rotate IDs, and maintain policy/consent correctness

This tiering is the core reason v0.1 remains permissive: adoption should start before we lock crypto/canonicalization.

---

## 6) “Future social media profile” fit (high level)

The Universal Manifest should power social/profile surfaces by treating “a profile” as a **projection**:

- A `publicProfile` shard can embed widely recognized vocab (e.g., `schema:Person`)
- `pointers` can link to federation identities (e.g., `activityPub.actor`, `matrix.userId`)
- `consents` govern whether a profile projection may be public/indexed

Concrete stub:

- `examples/v0.1/stubs/social-profile-manifest.jsonld`

---

## 7) Open depth (known big rocks)

These are the “depth” items that turn v0.1 into something broadly adoptable:

1. **Signature profile**
   - choose the first real signing envelope (and verification rules)
2. **Canonicalization**
   - define JSON-LD/RDF canonicalization expectations for signing
3. **Conformance suite**
   - add invalid fixtures + a conformance checklist for third parties
4. **Registry stabilization**
   - stabilize well-known shard/pointer/claim/consent names (and version them)
5. **Hosting/distribution**
   - publish the context/schema at stable URLs and document versioning guarantees

Track gaps in:

- `docs/AGENT-OBSERVED-GAPS.md`

---

## 8) Research depth (what’s currently imported)

There is substantially more background material in the LAN design library and prior archives; this repo currently imports a **focused subset** as design drivers:

### Federation / cross-property driver

- `research/federation/universal-manifest-workstream.md`
  - defines the “state capsule” framing and the minimum section set (claims/consents/devices/pointers/signature)

### LAN platform drivers (local-first reality)

- `research/lan-platform/lan-profile-architecture.md`
  - canonical vs projected state (Solid → Capsule), shards mapping, and why “profile” is a projection
- `research/lan-platform/lan-interoperability-sync.md`
  - update signaling and sync flows (push signal → fetch), offline behavior
- `research/lan-platform/lan-operational-runbooks.md`
  - enrollment, trust establishment, and operational procedures (venue/edge/display)
- `research/lan-platform/lan-appendices-and-standards-mapping.md`
  - standards mapping for adoption (DID, Solid, Matrix, Ed25519, canonicalization ideas)
- `research/lan-platform/lan-external-research-synthesis.md`
  - external synthesis and additional motivation context

These docs are **not normative**. When they imply a contract change, capture it in:

- `docs/DECISIONS.md`
