# 07 -- IWPS + UM: The Complete Portaling Stack

---

## The Analogy

Think of a shipping container on a cargo ship. The shipping company handles the transport -- routes, schedules, port negotiations, customs clearance. The container holds the cargo -- products, documentation, provenance labels. The shipping company does not define what goes in the container. The cargo owner does not build the ship. They are complementary: one handles *how things move*, the other handles *what moves*.

IWPS is the shipping company. Universal Manifest is the container.

---

## Why

IWPS (Inter-World Portaling Standard) defines *how* a user moves between virtual worlds: a two-call transport protocol (Query + Teleport) that handles capability negotiation, session binding, and communication paths between source and destination worlds.

But IWPS does not define *what* travels with the user. Its `assets` parameter is marked "Reserved for Future Use." It has no specification for how identity, consent, credentials, or preferences should be structured and carried during a portal event.

UM defines exactly this: a portable, signed, consent-aware JSON-LD document that carries the user's state. Neither standard is sufficient alone. Together, they form a complete portaling solution.

## What

The two-layer model:

| Layer | Standard | Responsibility |
|-------|----------|---------------|
| **Transport** | IWPS | Query + Teleport APIs, capability negotiation, session binding, communication paths |
| **Cargo** | UM | Identity, consent, facets, pointers, credentials, validity metadata, signatures |

IWPS handles "how do I get there?" UM handles "what comes with me?"

## How -- The Portal Flow

Here is what happens when a user portals from World A to World B with both standards operating together:

```
 Source World (A)                                     Destination World (B)
      |                                                      |
      |  1. User encounters a portal to World B              |
      |                                                      |
      |  2. Source calls IWPS Query API:                      |
      |     - portalURI = "worldb://lobby"                   |
      |     - userId = "did:key:z6Mk..."                     |
      |     - assets = { umid: "urn:uuid:abc-123" }          |
      |----------------------------------------------------->|
      |                                                      |
      |                 3. Destination receives the UMID,     |
      |                    fetches the manifest from          |
      |                    myum.net/urn:uuid:abc-123          |
      |                                                      |
      |                 4. Destination inspects the manifest: |
      |                    - Verifies signature (v0.2)        |
      |                    - Checks TTL / freshness           |
      |                    - Reads consent rules              |
      |                    - Resolves supported facets        |
      |                    - Resolves asset pointers          |
      |                                                      |
      |  5. Destination returns Query response:               |
      |     - approved = true                                 |
      |     - approvedAssets = [avatar, profile]              |
      |     - portalLimitations = [inventory: partial]        |
      |     - teleportId = "tport-xyz-789"                   |
      |<-----------------------------------------------------|
      |                                                      |
      |  6. Source calls IWPS Teleport API:                   |
      |     - teleportId = "tport-xyz-789"                   |
      |     - teleportPin = "pin-456"                        |
      |     - assets = { umid: "urn:uuid:abc-123" }          |
      |----------------------------------------------------->|
      |                                                      |
      |                 7. Destination loads the user with:   |
      |                    - Identity from subject DID        |
      |                    - Avatar from pointer URL          |
      |                    - Profile from publicProfile facet |
      |                    - Preferences from prefs.* keys    |
      |                    - Consent rules enforced           |
      |                      (default-deny)                   |
      |                                                      |
      |  8. Destination acknowledges arrival                  |
      |<-----------------------------------------------------|
```

### What UM adds to IWPS

| Gap in IWPS | What UM provides |
|-------------|-----------------|
| Asset transfer format (TBD) | Structured JSON-LD manifest with typed facets and asset pointers |
| Look-and-feel portability (TBD) | Avatar pointers, preference bundles, profile projection |
| Privacy and consent | Default-deny consent propagation; granular consent keys per facet |
| Portable state freshness | TTL via `issuedAt` / `expiresAt` timestamps |
| Cryptographic integrity | JCS + Ed25519 signatures (v0.2) |
| Compliance proofs | Claims and pointers for age-gate, KYC without exposing raw PII |

### What IWPS adds to UM

| Gap in UM | What IWPS provides |
|-----------|--------------------|
| Transport protocol for portaling | Query + Teleport two-call API with session binding |
| Capability negotiation | `portalLimitations` and `approvedAssets` in Query response |
| Communication path selection | Device, Cloud, Hybrid, User Agent models |
| Session binding | TeleportId + TeleportPin anti-replay mechanism |
| Operator trust tiers | OMA3 Security Certification (Bronze/Silver/Gold) |

### Key integration points

1. **`assets` parameter.** The IWPS `assets` field carries a UMID. The destination resolves it to a full manifest. No new fields needed on either side.

2. **`portalLimitations` maps to graceful degradation.** UM consumers are already required to project only what they support and ignore unknown fields. The destination's `portalLimitations` response tells the source which asset types it cannot support.

3. **IWPS `userId` maps to UM `subject`.** The `userId` in an IWPS request references the same DID that appears in the manifest's `subject` field. Transport-level identity binds to the rich portable state.

4. **User Agent path as UM carrier.** IWPS's User Agent communication model, where the user's client mediates the transfer, aligns with UM's subject-controlled consent model. The subject's wallet holds the manifest and selectively discloses facets.

### What this means for OMA3

IWPS and UM are not competing standards. They are complementary layers that together provide a complete portaling stack. UM fills the gaps that IWPS explicitly marks as TBD -- structured portable state, consent, integrity, and asset references -- without requiring changes to the IWPS API structure.

---

*Next: [08 -- Beyond Metaverse](08-what-else.md) shows the full breadth of UM's application space.*
