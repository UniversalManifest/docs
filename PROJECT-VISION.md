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

### Composite stack direction

The Universal Manifest should be treated as a **composite stack**, not as one giant all-knowing file format.

The stack has three cooperating layers:

- **Trust layer**: subject identifiers, issuer references, signatures, revocation/freshness signals, and other proof-bearing material.
- **Data layer**: portable records plus pointer-first references to external systems, stores, or artifacts.
- **Interaction layer**: consent, policy, audience/context rules, and relying-party exchange behavior.

This direction keeps UM storage-neutral and provider-neutral:

- the manifest carries portable state and references,
- large or volatile data stays outside the manifest,
- consumers can project the parts they understand without requiring one universal backend.

The Universal Manifest should treat a **Record** as the core primitive:

- A record can be a **leaf** (single unit of data) or a **container** with nested sub-records.
- Records are intended to be manageable “packets/maps” of information (for example: public profile, proof-of-personhood evidence, game profile).
- Records should support **push** and **request/pull** exchange between systems.
- A record may declare its own standards/syntax/schema, enabling a multi-schema ecosystem instead of one global rigid schema.

### Source-of-truth and active-runtime direction

The manifest is not only a static document shape. Real deployments often require a **subject-controlled active runtime** (for example: wallet, client, agent, or local-first sync service) that does all of the following:

- maintains the subject's current source of truth,
- mediates consent and disclosure,
- resolves or updates pointers to external systems,
- coordinates **push** notifications and **pull/request** retrieval flows,
- operates bridge adapters for open protocols or closed surfaces when needed.

This runtime direction is non-normative architecture guidance, not a requirement that every conformant implementation ship the same client model.

Common loop shape:

1. observe local or external state change,
2. signal or receive update intent,
3. fetch or assemble the required manifest state,
4. verify freshness and trust posture,
5. project allowed data to the relying surface,
6. revoke, refresh, or withdraw access when policy changes.

### Pointer-first storage separation

Universal Manifest should remain pointer-first:

- the manifest defines **what** is being asserted or referenced,
- external systems, pods, nodes, ledgers, or service endpoints hold **where** larger or mutable data lives,
- the subject runtime governs how those references are refreshed, shared, or revoked over time.

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
  - `Metaverse Universal Manifest (MUM) concept source document (Metaverse Standards Forum working group archive)`

Strategic direction:

- Keep metaverse portability as a first-class integration lane while positioning Universal Manifest as a broader cross-domain standard.
- Treat **portaling** as the concrete metaverse portability experience: a subject jumps between different worlds or platforms while the manifest carries the identity, content pointers, and policy state that the destination surface is allowed to project.
- Add an explicit integration lane for **RP1 spatial fabric** use cases (spatial context, place anchoring, and cross-world portability).
- Add an explicit integration lane for **smart-glasses social layer** use cases, including:
  - face-visibility permissions for recordings
  - automatic public social-profile disclosure controls
  - context-sensitive disclosure and consent for real-world + smart-glasses interactions

Additional integration lanes (2026-02-20):

- Add an explicit integration lane for **multi-provider proof-of-personhood** credential binding, targeting World ID, Gitcoin Passport, and BrightID as initial providers with complementary verification approaches (biometric, composite-score, and social-graph).
- Add an explicit integration lane for **Chia blockchain DID/VC credential attestation**, supporting `did:chia` as a self-sovereign identity anchor and on-chain Verifiable Credentials as provenance-verifiable claim extensions.

Boundary policy:

- These are source-of-truth vision directives and integration targets.
- They do **not** become normative spec requirements until implemented via versioned spec/conformance changes and decision records.

## Follow-on direction from localized source wave (2026-03-06)

The newly localized corpus reinforces four architecture boundaries that should remain explicit:

- Universal Manifest is a portable pointer-and-policy envelope, not a monolithic database replacement.
- Composite-stack framing (trust, data, interaction) is the preferred architecture language for future integrations.
- Local-first or subject-controlled runtimes are valid implementation patterns for synchronizing state across open and closed surfaces.
- Protocol recommendations in integration lanes must remain bounded and non-locking when upstream ecosystems are volatile.
