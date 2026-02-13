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

## CEO architectural direction (vision input)

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

Note:

- This section is **vision direction**, not yet normative contract text. Normative requirements must be added through versioned spec docs and decision records.
