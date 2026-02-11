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

