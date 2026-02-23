# Project Vision — Universal Manifest

## Goal

Define a **portable manifest** format that can be handed between compatible apps/devices to establish:

- **Subject**: who the manifest is about (stable identifier references)
- **Claims**: roles, permissions, verification state, entitlements
- **Consents**: per-surface or per-property privacy controls
- **Devices**: registered devices + trust levels
- **Pointers**: links to canonical sources (e.g., Pod URL, Matrix ID) without embedding large data
- **Integrity**: signatures + short TTL + explicit revocation signals (later)

## Non-goals (near-term)

- Selecting a DID method/provider as a hard dependency (must function without DID).
- Shipping a full cryptography suite implementation in this repo.
- Encoding large media payloads inside the manifest.

## Current status

- v0.1 is a draft target (structure + semantics + examples).

## Architectural direction (vision input)

The Universal Manifest should treat a **Record** as the core primitive:

- A record can be a **leaf** (single unit of data) or a **container** with nested sub-records.
- Records are intended to be manageable “packets/maps” of information (for example: public profile, proof-of-personhood evidence, game profile).
- Records should support **push** and **request/pull** exchange between systems.
- A record may declare its own standards/syntax/schema, enabling a multi-schema ecosystem instead of one global rigid schema.

Permission model direction:

- Records and attributes should support explicit visibility states (at minimum `public` and `private`, with room for additional states such as `restricted`/`permissioned`).
- Field-level permissions can differ across records (example: date of birth handling varies by use case and policy).

Research direction:

- Capture these as repeatable architectural patterns and benchmark public implementations/protocols to refine the model before locking normative spec behavior.

Validation direction:

- Build a suite of **user journeys** that represent real adopter flows (issuer → exchange → consumer behavior).
- Map each journey to one or more executable tests and run them as a single test suite to prove the Universal Manifest concept works end-to-end (not just schema validation).
- Treat this journey-driven test suite as required evidence toward “done done” for production-candidate and world-ready claims.

Note:

- This section is **vision direction**, not yet normative contract text. Normative requirements must be added through versioned spec docs and decision records.

## Lineage and expansion direction (2026-02-20)

Lineage source:

- Universal Manifest is explicitly descended from the earlier **Metaverse Universal Manifest (MUM)** concept document:
  - `/Users/grig/work/MSF - Metaverse Standards Forum/repo/msf-wg-tool/geopose-talk/INBOX/Use Case_ Metaverse Universal Manifest - v1.0.md`

Strategic direction:

- Keep metaverse portability as a first-class integration lane while positioning Universal Manifest as a broader cross-domain standard.
- Add an explicit integration lane for **RP1 spatial fabric** use cases (spatial context, place anchoring, and cross-world portability).
- Add an explicit integration lane for **smart-glasses AR social layer** use cases, including:
  - face-visibility permissions for recordings
  - automatic public social-profile disclosure controls
  - context-sensitive disclosure and consent for real-world + AR interactions

Additional integration lanes (2026-02-20):

- Add an explicit integration lane for **multi-provider proof-of-personhood** credential binding, targeting World ID, Gitcoin Passport, and BrightID as initial providers with complementary verification approaches (biometric, composite-score, and social-graph).
- Add an explicit integration lane for **Chia blockchain DID/VC credential attestation**, supporting `did:chia` as a self-sovereign identity anchor and on-chain Verifiable Credentials as provenance-verifiable claim extensions.

Boundary policy:

- These are source-of-truth vision directives and integration targets.
- They do **not** become normative spec requirements until implemented via versioned spec/conformance changes and decision records.
