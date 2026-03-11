# Universal Manifest -- Full Briefing for AI Agents

## Purpose of This Document

This document gives you, an AI agent, everything you need to understand what Universal Manifest is, what it can do, and where it could go. After reading this, you should be able to reason about new scenarios, integration lanes, and applications for the standard.

---

## 1. What Universal Manifest Is

**Universal Manifest (UM)** is a portable, cryptographically verifiable state capsule standard. It is a single JSON-LD document -- a *manifest* -- that can be handed between any combination of apps, devices, services, and platforms to convey:

- **Identity references** -- who or what the manifest is about
- **Claims** -- roles, permissions, verification status, entitlements
- **Consents** -- per-surface and per-property privacy controls
- **Devices** -- registered endpoints and their trust levels
- **Pointers** -- URL references to canonical data sources (without embedding large payloads)
- **Facets** -- composable, named sub-documents that carry domain-specific data
- **Signatures** -- cryptographic integrity seals that prove authenticity without central authorities

Think of Universal Manifest the way you think of HTTP for transport or JSON-LD for linked data: **UM is the standard envelope for portable identity, state, and capability across any system boundary.**

UM is not tied to any platform, identity provider, storage layer, framework, or blockchain. It works with DIDs but does not require them. It works with Verifiable Credentials but does not depend on them. It works offline. It works at the edge. It works in browsers, on constrained devices, in metaverse engines, on smart glasses, and in server-to-server flows.

---

## 2. The Core Contract

A Universal Manifest is a JSON-LD object with a predictable shape. Here is what it contains:

### Required Fields (every manifest)

| Field | Purpose |
|---|---|
| `@context` | JSON-LD context URI pointing to the UM vocabulary |
| `@id` | Globally unique manifest identifier (URI; recommended `urn:uuid:...`) |
| `@type` | Must include `um:Manifest` (string or array) |
| `manifestVersion` | Spec version (e.g., `"0.1"` or `"0.2"`) |
| `subject` | Who/what this manifest is about (URI; recommended DID, but any stable URI works) |
| `issuedAt` | ISO 8601 timestamp -- when the manifest was created |
| `expiresAt` | ISO 8601 timestamp -- when the manifest expires (TTL enforcement is mandatory) |

### Optional Fields

| Field | Purpose |
|---|---|
| `facets` | Array of composable sub-documents (`um:Facet`) -- named data sections |
| `claims` | Roles, permissions, verification assertions |
| `consents` | Privacy and disclosure controls |
| `devices` | Registered device endpoints and trust levels |
| `pointers` | URL references to canonical external data sources |
| `signature` | Cryptographic signature (permissive in v0.1, profiled in v0.2) |

### Facets

Facets are the primary composition mechanism. Each facet is a named container that can:
- **Embed** entity data directly (inline JSON-LD)
- **Reference** external data via a `ref` URI
- Carry any domain-specific payload without affecting the core manifest shape

A single manifest might contain a `publicProfile` facet, a `deviceRegistration` facet, a `crossWorldProfile` facet, and a `spatialAnchors` facet -- all coexisting without conflict.

### Pointers

Pointers are lightweight URL references to authoritative data sources. Instead of copying an entire user profile into the manifest, you add a pointer:

```json
{ "name": "activityPub.actor", "url": "https://mastodon.social/@alice" }
```

Consumers that understand ActivityPub can follow the pointer. Consumers that do not simply ignore it.

### Forward Compatibility

Consumers MUST safely ignore unknown fields. This is the rule that makes the whole system work: early adopters can extend manifests with new fields, facets, and pointers without breaking any existing consumer. Unknown top-level properties, unknown facet shapes, unknown claim types, unknown pointer names -- all are tolerated.

### Versioning

Versions use immutable, numbered paths. Once published, a version's artifacts never change. Breaking changes require a new version folder (e.g., `v0.1` to `v0.2`). Additive changes (new optional fields, new registry entries) can happen within a minor version.

---

## 3. What v0.2 Adds -- Cryptographic Verification

v0.1 is a permissive placeholder: the `signature` field exists but has no interoperable verification profile. v0.2 locks that down with a production-grade signature system:

### Signature Profile: JCS + Ed25519

- **Canonicalization**: JSON Canonicalization Scheme (JCS, RFC 8785) -- deterministic JSON byte representation
- **Algorithm**: Ed25519 -- fast, compact, widely implemented public-key signatures
- **Encoding**: base64url for signature values
- **Key material**: referenced via `signature.keyRef` (DID URL or HTTPS URL) or embedded via `signature.publicKeySpkiB64` for offline/local-first verification

### How Signing Works

1. Start with the manifest JSON object
2. Remove the `signature` property entirely
3. Canonicalize the remaining object using JCS (RFC 8785) to produce deterministic UTF-8 bytes
4. Compute Ed25519 signature over those bytes
5. Attach the signature back to the manifest

### How Verification Works

1. Confirm the document is a valid UM manifest
2. Check TTL: reject if `now > expiresAt`
3. Confirm `signature.algorithm === "Ed25519"` and `signature.canonicalization === "JCS-RFC8785"`
4. Obtain the public key (from `publicKeySpkiB64` or by resolving `keyRef`)
5. Recompute signing input (remove `signature`, JCS canonicalize)
6. Verify Ed25519 signature over canonical bytes

If verification fails, the manifest is rejected.

### What This Enables

- **Tamper detection**: any modification to any field invalidates the signature
- **Trust without centralized authorities**: verification uses public-key cryptography, not a phone-home to a central server
- **Offline verification**: with `publicKeySpkiB64`, verification works entirely locally
- **Revocation-aware verification**: optional `statusRef` and `revocationCursor` fields support checking whether a manifest has been revoked
- **Profile extensibility**: future algorithms (post-quantum, Data Integrity / RDF canonicalization) can be added as new profile pairs without breaking existing consumers

---

## 4. Resolution -- UMIDs and myum.net

Every manifest has a globally unique identifier (`@id`). These identifiers -- UMIDs -- can be resolved through the UM resolver at `myum.net`.

### How Resolution Works

```
https://myum.net/{UMID}
```

The resolver provides:
- **Deterministic lookup**: the same UMID always resolves to the same manifest
- **Direct return or redirect**: either `200` with the manifest payload, or `302`/`307` redirect to the canonical manifest URL
- **Clear error semantics**: `404` for unknown UMIDs, `410` for revoked/removed manifests
- **Integrity metadata**: hash, signature profile, issued/expires when available
- **Decentralized authoring**: the resolver indexes externally hosted manifests -- it does not require centralized authoring

### Domain Architecture

The project uses two domains with distinct responsibilities:

| Domain | Purpose |
|---|---|
| `universalmanifest.net` | Standards domain -- spec artifacts, documentation, vocabulary files, governance |
| `myum.net` | Resolver domain -- runtime UMID lookup and manifest retrieval |

This separation keeps the specification neutral and governance-clean, while runtime resolution concerns are isolated in their own service.

---

## 5. Real-World Examples -- What Manifests Look Like

### Minimal v0.1 Manifest (simplest valid document)

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld",
  "@id": "urn:uuid:2b5f0d3c-3c4c-4b83-8f2a-6f3b2cbd5c7d",
  "@type": "um:Manifest",
  "manifestVersion": "0.1",
  "subject": "did:key:z6MkpExampleSubjectDid",
  "issuedAt": "2026-02-11T20:45:58Z",
  "expiresAt": "2026-02-12T20:45:58Z",
  "facets": []
}
```

### Signed v0.2 Manifest (with Ed25519 signature and a profile facet)

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld",
  "@id": "urn:uuid:11111111-1111-4111-8111-111111111111",
  "@type": "um:Manifest",
  "manifestVersion": "0.2",
  "subject": "did:example:alice",
  "issuedAt": "2026-02-17T00:00:00.000Z",
  "expiresAt": "2026-02-18T00:00:00.000Z",
  "facets": [
    {
      "@type": "um:Facet",
      "name": "publicProfile",
      "entity": {
        "@id": "did:example:alice",
        "@type": "schema:Person",
        "name": "Alice Example"
      }
    }
  ],
  "signature": {
    "algorithm": "Ed25519",
    "canonicalization": "JCS-RFC8785",
    "keyRef": "did:example:alice#key-1",
    "created": "2026-02-17T00:00:00.000Z",
    "publicKeySpkiB64": "MCowBQYDK2VwAyEAvWsBD/ov/5zQwtkxvssqOFz/Ejca8C0NfnAJ9z0iBZY=",
    "value": "0fe9Moud3n6j50rN7pcGgxAsxMLpGPvvxID1jjs5a7cJVCc08XI8tO19G_bFnJ86h8zqJWQA2sLMziSAmUL3CQ"
  }
}
```

### Signed v0.2 Manifest with Facets (venue with device registration)

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld",
  "@id": "urn:uuid:44444444-4444-4444-8444-444444444444",
  "@type": "um:Manifest",
  "manifestVersion": "0.2",
  "subject": "did:example:venue-edge",
  "issuedAt": "2026-02-27T00:00:00.000Z",
  "expiresAt": "2026-02-28T00:00:00.000Z",
  "facets": [
    {
      "@type": "um:Facet",
      "name": "venueProfile",
      "entity": {
        "@id": "did:example:venue-edge",
        "@type": "schema:Place",
        "name": "Example Venue",
        "description": "A demonstration venue for Universal Manifest"
      }
    },
    {
      "@type": "um:Facet",
      "name": "deviceRegistration",
      "ref": "https://example.pod.provider/devices/tv-001",
      "entity": {
        "@id": "urn:uuid:device-tv-001",
        "@type": "um:Entity",
        "name": "Display Device TV-001",
        "description": "Public display device enrolled to venue edge"
      }
    }
  ],
  "signature": {
    "algorithm": "Ed25519",
    "canonicalization": "JCS-RFC8785",
    "keyRef": "did:example:venue-edge#key-1",
    "created": "2026-02-27T00:00:00.000Z",
    "publicKeySpkiB64": "MCowBQYDK2VwAyEAvWsBD/ov/5zQwtkxvssqOFz/Ejca8C0NfnAJ9z0iBZY=",
    "value": "NkTRGYGG7jELyXFlaqFsLnkVs7E88dQ5lYL9Q1yMz4nsr9zsog9urjxQa25UNV2_REHfhqMX1_Q_Uf1Y6eXfDg"
  }
}
```

### Rich Manifest -- Metaverse Cross-World Profile (with claims, consents, pointers, and facets)

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld",
  "@id": "urn:uuid:7b8c9d0e-4444-4a3d-8a11-0dbf2ce44210",
  "@type": "um:Manifest",
  "manifestVersion": "0.1",
  "subject": "did:example:metaverse-user-01",
  "issuedAt": "2026-02-20T05:20:00Z",
  "expiresAt": "2026-02-21T05:20:00Z",
  "claims": [
    { "@type": "um:Claim", "name": "metaverse.role", "value": "creator" }
  ],
  "consents": [
    { "@type": "um:Consent", "name": "metaverse.profilePublic", "value": "allowed" },
    { "@type": "um:Consent", "name": "metaverse.socialGraphShare", "value": "restricted" },
    { "@type": "um:Consent", "name": "metaverse.voiceCapture", "value": "denied" }
  ],
  "pointers": [
    { "name": "metaverse.profile", "url": "https://example.com/metaverse/profiles/user-01" },
    { "name": "metaverse.avatar", "url": "https://example.com/metaverse/avatars/user-01" },
    { "name": "metaverse.inventory", "url": "https://example.com/metaverse/inventory/user-01" },
    { "name": "metaverse.socialGraph", "url": "https://example.com/metaverse/social/user-01" }
  ],
  "facets": [
    {
      "@type": "um:Facet",
      "name": "crossWorldProfile",
      "entity": {
        "@type": ["um:Entity", "metaverse:CrossWorldProfile"],
        "displayName": "Nova",
        "homeWorld": "world://origin.example/home",
        "supportedWorlds": [
          "world://origin.example/home",
          "world://gallery.example/arcade"
        ]
      }
    }
  ],
  "signature": {
    "algorithm": "Ed25519",
    "keyRef": "did:example:metaverse-user-01#key-1",
    "value": "BASE64URL_SIGNATURE_PLACEHOLDER"
  }
}
```

---

## 6. Integration Lanes Already Explored

Universal Manifest has active integration guidance for nine distinct lanes. Each demonstrates how the standard envelope adapts to a radically different domain without changing the core spec.

### 6.1 Social Profiles (ActivityPub, Bluesky, Mastodon)

**Scenario**: A creator named Jules publishes a single manifest that carries their public profile (`schema:Person`), consent for public display, and pointers to their ActivityPub actor, Solid Pod, and Matrix identity. Any compatible social surface -- a Mastodon instance, a Bluesky client, a web profile page, or a venue display screen -- can receive the manifest, read the facets it understands, follow the pointers it supports, and render an appropriate projection. The same manifest drives a rich web profile page, a compact venue screen card, and a federated social identity -- all from one document.

**Key fields used**: `facets` (publicProfile with `schema:Person`), `pointers` (activityPub.actor, solidPod, matrix.userId), `consents` (social.profilePublic, publicDisplay).

### 6.2 Smart Glasses (Consent-First Overlay Controls)

**Scenario**: Alex walks into a conference wearing smart glasses. Their manifest declares: face recording is denied, public professional profile may be auto-shared, and voice capture is not permitted. When other attendees' glasses encounter Alex, the smart glasses runtime fetches Alex's manifest, checks consent keys, and enforces the policy in real time -- blurring Alex's face in recordings, surfacing their professional badge in the overlay, and muting voice capture streams. The consent model is context-sensitive: the same person might allow face visibility at a family event but deny it at a public conference.

**Key consent keys**: `ar.recording.faceVisible`, `ar.recording.voiceAllowed`, `ar.profile.autoSharePublic`, `ar.profile.autoShareProfessional`, `ar.overlay.presenceVisible`.

### 6.3 Metaverse (Cross-World Identity Portability)

**Scenario**: A user named Nova has a persistent identity across multiple virtual worlds. Their manifest carries a cross-world profile facet listing their home world, supported worlds, avatar reference, inventory endpoint, and social graph. When Nova moves from one virtual world to another, the target world resolves their manifest, verifies it, and projects their identity -- importing reputation, restoring inventory references, and applying consent gates for voice capture and social graph sharing. The manifest is the portable identity layer that makes cross-world movement seamless.

**Key fields used**: `pointers` (metaverse.profile, metaverse.avatar, metaverse.inventory, metaverse.socialGraph), `consents` (metaverse.profilePublic, metaverse.socialGraphShare, metaverse.voiceCapture), `facets` (crossWorldProfile).

### 6.4 RP1 Spatial Fabric (Physical-Digital Spatial Anchoring)

**Scenario**: A spatial computing platform anchors digital content to physical locations. A venue publishes a manifest with spatial anchor facets that define where digital experiences are attached to real-world coordinates. A visitor's smart glasses device resolves the venue manifest, reads the spatial anchor data, and renders location-pinned content. Consent gates control whether the visitor's location is persisted, whether cross-world spatial linking is allowed, and whether session replay is permitted.

**Key pointer names**: `rp1.fabric`, `rp1.anchorSet`, `rp1.placeGraph`, `rp1.sessionContext`. **Key consent keys**: `spatial.locationShare`, `spatial.anchorShare`, `spatial.crossWorldLinking`.

### 6.5 OMATrust (Trusted Asset Lifecycle Management)

**Scenario**: A digital service publishes a manifest carrying OMATrust attestation claims -- proof-based trust scores, attester endorsements, security assessment status, and lifecycle state (active, revoked, superseded). Consumers evaluate the trust posture using claims and pointers to OMATrust verification endpoints, without the manifest itself needing to embed the full attestation chain. The lifecycle facet tracks revocation and supersession events, enabling consumers to make deterministic trust decisions.

**Key claims**: `omatrust.policy.trustMode`, `omatrust.proof.type`, `omatrust.attestation.endorsement`, `omatrust.attestation.securityAssessment.status`. **Key pointers**: `omatrust.reputation.attestation`, `omatrust.reputation.verify`, `omatrust.lifecycle.revocationLog`.

### 6.6 DID + VC (Decentralized Credential Verification)

**Scenario**: A user anchors their identity to a Chia blockchain DID (`did:chia`) and carries on-chain Verifiable Credential attestations in their manifest. The manifest's `subject` is a `did:chia` identifier. Claims include VC proof hashes that can be verified against the Chia blockchain transaction history. Consumers that support Chia can verify attestation integrity on-chain; consumers that do not simply ignore the Chia-specific claims and use the rest of the manifest normally.

**Key pointers**: `chia.wallet.address`, `chia.vc.attestation`, `chia.did.document`, `chia.vc.proofHash`. **Key consent keys**: `chia.credentialShare`, `chia.onChainPublish`, `chia.walletDisclosure`.

### 6.7 Proof of Personhood (World ID, Gitcoin Passport, BrightID)

**Scenario**: A user accumulates personhood verification from three independent providers: an iris-scan attestation from World ID (biometric), a composite trust score from Gitcoin Passport (multi-source aggregation), and a social-graph uniqueness attestation from BrightID. All three coexist as claims in a single manifest, each using its own namespace prefix. A consuming platform selects which providers it trusts, applies its own threshold logic, and ignores providers it does not recognize. No single provider is required -- a manifest might carry zero, one, or all three.

**Namespace prefixes**: `personhood.worldId.*`, `personhood.gitcoinPassport.*`, `personhood.brightId.*`. **Key consent keys**: `personhood.shareVerification`, `personhood.crossPlatformLink`, `personhood.providerDisclosure`.

### 6.8 IoT/Edge Devices (Venue Beacons, Sensors, Displays)

**Scenario**: A cafe enrolls a public display device (e.g., an Android TV). The venue edge issues a device-scoped manifest that encodes the device identity, capabilities (rendering support, max resolution), venue association, content policy (safe mode rating, allowed/blocked content tags), and operational pointers (edge base URL, discovery descriptor). The display receives manifest-changed signals, fetches by ID, caches while in use, and enforces TTL. Telemetry logs reference manifest IDs, not full payloads. The display operates in local-first mode -- no cloud dependency required.

**Key fields used**: `devices` (enrolled hardware), `claims` (role, policy.safeMode), `consents` (telemetry.proofOfPlay), `pointers` (edgeBaseUrl, edgeDescriptor, universalManifest.current).

### 6.9 Reference Runtime (Edge-Display-Admin Capsule Flow)

**Scenario**: A reference implementation demonstrates the full three-role flow. The **edge** (venue server) issues manifests for venues, devices, and creators, rotates UMIDs per issuance, and serves local discovery plus retrieval routes. The **display** (constrained consumer like an Android TV) receives update signals, fetches manifests by ID, caches with TTL enforcement, and logs by reference. The **admin** (ops dashboard) enrolls displays, configures policy, and views current manifest state. Push-signal-then-pull-fetch transport keeps the architecture simple and offline-resilient.

**Transport model**: mDNS discovery (`_um-edge._tcp.local`), well-known descriptor (`/.well-known/um/edge.json`), push signal with `displayId` + `manifestId`, pull fetch by manifest ID.

---

## 7. What Makes Universal Manifest Powerful

These are the design properties that enable UM to work across such diverse domains:

### Platform-Agnostic
UM works anywhere JSON-LD works. No framework dependency, no runtime requirement, no platform lock-in. If a system can parse JSON, it can consume a manifest.

### Signature-Optional
v0.1 is permissive -- adopt the format today without implementing cryptography. v0.2 adds Ed25519 signatures when trust and tamper protection are needed. The same manifest shape works at both levels.

### Forward-Compatible
Unknown fields are preserved, not rejected. This is a normative requirement. It means any consumer built today will continue to work with manifests from the future, even if those manifests contain fields the consumer has never seen.

### Local-First
Manifests are self-contained documents with TTL-based validity windows. No phone-home is required. Verification can happen entirely offline when public key material is embedded. Caching is built into the contract. This makes UM work on constrained devices, in low-connectivity environments, and at the network edge.

### Projection-Capable
One manifest, many consumer views. A social platform reads the `publicProfile` facet. A venue display reads the `publicCapsule` facet. A spatial computing engine reads the `spatialAnchors` facet. Each consumer projects the manifest into the view it needs, ignoring everything else.

### Verifiable
v0.2 signatures prove authenticity without a central authority. The signing input is deterministic (JCS canonicalization). Verification is portable (Ed25519 is implemented in every major language). Revocation-aware verification is available when needed.

### Resolvable
UMIDs provide stable, deterministic lookup via `myum.net/{UMID}`. Any manifest can be fetched by its identifier from anywhere. The resolver is decentralized in authoring -- it indexes externally hosted manifests.

### Composable
Manifests can reference other manifests. Facets can embed entities or reference them via URI. Pointers link to canonical external sources. This enables a graph of interconnected state capsules without monolithic documents.

---

## 8. Real-World Analogies

To build intuition for how Universal Manifest works:

**A manifest is like a passport** that any border crossing can read. It has a standard shape with a fixed header (your name, photo, nationality, issue date, expiry date) and variable content. Any country in the world knows how to process it, even though each country has different rules.

**Facets are like pages in that passport.** One page might hold your visa for Japan, another your vaccination record, another your driver's license endorsement. Each page carries domain-specific data, but they all fit inside the same passport.

**Pointers are like visa stamps that reference external systems.** A visa stamp does not contain the entire immigration database of the issuing country -- it contains a reference number that the border crossing can look up if needed. Pointers work the same way: they link to authoritative external data without embedding it.

**Signatures are like the holographic seal** that proves the passport is genuine. Without the seal, you have a document that looks right but could be forged. With the seal, any inspector can verify authenticity using standardized equipment (public key cryptography instead of UV light).

**Resolution is like looking up a passport number** to get the full record. Given a UMID, any system can query `myum.net` to retrieve the manifest, just as any immigration system can look up a passport number to retrieve the holder's record.

**Consent keys are like the stamped permissions pages** where you declare what border crossings may do with your data -- whether they can share your entry record, photograph your face, or store your biometrics.

**TTL (time-to-live) is like the expiration date** on the passport itself. After the expiry, the document must not be used to grant permissions or access -- even if the holder is still the same person.

---

## 9. The Breadth of Possibility

Universal Manifest is designed for any system that needs portable, verifiable state about an entity. The integration lanes explored so far demonstrate breadth, but they only scratch the surface. Consider these domains:

### Healthcare
**Patient consent capsules.** A patient publishes a signed manifest carrying consent facets for each healthcare provider: which procedures are authorized, which data may be shared, which emergency contacts are valid. The manifest travels with the patient across hospitals, clinics, and pharmacies. Each provider reads the consent facets it needs and ignores the rest. TTL ensures stale consent is never honored. Signatures prove the consent has not been tampered with.

### Supply Chain
**Product provenance manifests.** Every physical product carries a manifest that traces its origin, manufacturing steps, certifications, and chain-of-custody. A coffee bag's manifest includes facets for farm origin, organic certification, roasting date, and fair-trade attestation. Retailers resolve the manifest to verify provenance. Consumers scan a QR code to see the full chain. Signatures prevent counterfeiting claims.

### Gaming
**Cross-game character and inventory portability.** A player's manifest carries their character profile, achievement history, inventory references, and reputation across multiple games. When the player enters a new game, the game engine resolves their manifest, reads the facets it supports (character cosmetics, earned titles, transferable items), and applies consent gates for what may be imported. The player's identity and progress move between games without each game needing bilateral integration with every other game.

### Education
**Credential and certification portability.** A student's manifest carries facets for each credential: university degrees, professional certifications, course completions, skill assessments. Each credential facet references the issuing institution via pointers and carries verification claims. Employers resolve the manifest to verify credentials. The student controls which credentials are visible to which consumers via consent keys.

### Government
**Digital identity capsules.** A citizen's manifest carries government-issued identity claims, voter registration status, tax filing references, and service entitlements. Each government agency reads only the facets relevant to its function. Cross-border scenarios use the same manifest shape, with each country's agencies reading the claims they recognize and ignoring the rest. Signatures ensure the identity claims have not been forged.

### Creative Economy
**Creator attribution and rights management.** An artist publishes a manifest for each creative work: authorship claims, license terms, revenue-sharing pointers, exhibition history, and provenance chain. Galleries, streaming platforms, and NFT marketplaces all resolve the same manifest. The artist controls attribution and licensing through consent keys. Signatures prove the attribution has not been tampered with.

### AI Agents
**Agent capability and authorization manifests.** An AI agent publishes a manifest declaring its capabilities, authorization scope, rate limits, data access permissions, and accountability chain. When the agent interacts with a service, the service resolves the agent's manifest to verify what the agent is authorized to do. Claims encode capability boundaries. Consent keys control what data the agent may access. Signatures prove the manifest was issued by the agent's operator. TTL ensures stale authorizations expire.

### Digital Twins
**Physical-digital entity state capsules.** A building, vehicle, or piece of industrial equipment publishes a manifest carrying its current operational state, maintenance history, sensor readings, and compliance certifications. Maintenance crews, insurance providers, and regulatory auditors each read the facets relevant to their function. Pointers reference live telemetry endpoints. Signatures ensure the state report is authentic.

### Event and Venue Management
**Attendee capability capsules.** An event attendee carries a manifest with their ticket entitlements, VIP access claims, dietary preference facets, and accessibility requirement declarations. Venue staff, food vendors, and session organizers each read the relevant sections. The same manifest works at a music festival, a corporate conference, and a sports stadium.

### Decentralized Finance
**Portable compliance and KYC capsules.** A DeFi user carries a manifest with KYC verification claims from multiple providers, accredited investor attestations, and jurisdictional compliance facets. Each protocol reads the compliance claims it requires. The user does not need to repeat KYC for every new protocol -- the manifest is the portable proof.

---

## 10. Existing Fixture Coverage

The repository includes a rich set of example manifests that demonstrate the standard across domains:

**Core fixtures:**
- `minimal-manifest.jsonld` -- bare-minimum valid manifest
- `type-array-manifest.jsonld` -- `@type` as array
- `unknown-fields-manifest.jsonld` -- forward-compatibility demonstration
- `manifest-with-facets.jsonld` -- facet composition (embedded + referenced)

**Domain-specific stubs:**
- `venue-edge-manifest.jsonld` -- venue identity, policy, edge node, enrolled devices
- `display-device-manifest.jsonld` -- constrained consumer (public display device) with capabilities
- `creator-public-capsule-manifest.jsonld` -- creator profile with public capsule projection
- `social-profile-manifest.jsonld` -- portable public profile for social surfaces
- `display-envelope-manifest.jsonld` -- minimal display without DID dependency

**Integration lane stubs:**
- `metaverse-crossworld-profile-manifest.jsonld` -- metaverse portaling and cross-world identity portability
- `rp1-spatial-fabric-manifest.jsonld` -- spatial anchoring and place graph
- `smart-glasses-consent-allowed-manifest.jsonld` -- smart glasses consent (allowed)
- `smart-glasses-consent-denied-manifest.jsonld` -- smart glasses consent (denied)
- `mastodon-personhood-multi-credential-manifest.jsonld` -- Mastodon + multi-provider personhood
- `bluesky-personhood-multi-credential-manifest.jsonld` -- Bluesky + multi-provider personhood
- `multi-did-method-coverage-manifest.jsonld` -- multiple DID method support
- `did-vc-credential-lane-manifest.jsonld` -- Chia blockchain DID/VC
- `oma-trust-proof-based-service-manifest.jsonld` -- OMATrust proof-based attestation
- `oma-trust-trusted-attester-service-manifest.jsonld` -- OMATrust trusted attester
- `oma-trust-lifecycle-edge-service-manifest.jsonld` -- OMATrust lifecycle management

**Signed v0.2 fixtures:**
- `minimal-signed-manifest.jsonld` -- minimal signed manifest with Ed25519
- `manifest-with-facets-signed.jsonld` -- signed manifest with venue profile and device facets
- `manifest-with-pointers-signed.jsonld` -- signed manifest with pointer references
- `manifest-with-revocation-metadata.jsonld` -- signed manifest with revocation support

---

## 11. Architecture Summary

```
+---------------------+      +------------------+      +-------------------+
|   ISSUER            |      |   MANIFEST       |      |   CONSUMER        |
|   (produces)        | ---> |   (portable      | ---> |   (verifies +     |
|                     |      |    state capsule) |      |    projects)      |
+---------------------+      +------------------+      +-------------------+

  - Generates UMID             - JSON-LD document        - Validates structure
  - Sets subject               - Required header         - Enforces TTL
  - Adds claims/consents       - Optional facets         - Verifies signature
  - Signs with Ed25519         - Optional pointers       - Reads known facets
  - Publishes / delivers       - Optional claims         - Follows pointers
                               - Optional consents       - Ignores unknowns
                               - Optional devices        - Projects to surface
                               - Optional signature

+---------------------+      +------------------+
|   RESOLVER          |      |   SPEC DOMAIN    |
|   myum.net/{UMID}   |      |   universalmanifest.net
|   - deterministic    |      |   - JSON-LD context
|     lookup           |      |   - JSON Schema
|   - 200 or redirect  |      |   - Conformance docs
|   - 404 / 410 errors |      |   - Vocabulary
+---------------------+      +------------------+
```

---

## 12. Key Design Principles (Why These Choices Matter)

1. **Envelope, not database.** A manifest is a lightweight capsule, not a data lake. It carries references and summaries, not entire datasets. This keeps manifests small, fast to transmit, and safe to cache.

2. **Consent is structural, not decorative.** Consent keys are first-class fields in the manifest, not metadata annotations. Consumers are expected to default to deny when consent is missing.

3. **TTL is mandatory, not optional.** Every manifest has an expiration. There is no "forever valid" manifest. This prevents stale state from persisting indefinitely and provides a basic defense against replay attacks.

4. **Signatures are additive, not breaking.** v0.1 works without signatures. v0.2 adds them. Future versions can add new signature profiles. The transition from unsigned to signed does not break existing consumers.

5. **Facets are the extension mechanism.** Instead of growing the core spec with domain-specific fields, UM uses facets. Any domain can define its own facet shapes without touching the core vocabulary. This is how UM scales from IoT devices to metaverse engines to healthcare systems.

6. **Pointers avoid data duplication.** Instead of embedding a full ActivityPub actor document or a complete inventory list, the manifest points to the authoritative source. This keeps the manifest small and the data authoritative.

7. **The spec is a contract, not a framework.** UM defines the document shape and the verification rules. It does not prescribe how you store, transport, or render manifests. Cloudflare Workers, IPFS, local SQLite databases, Bluetooth beacons -- any transport and storage mechanism works.

---

## Summary

Universal Manifest is a portable, cryptographically verifiable state capsule standard built on JSON-LD. It provides a standard envelope for identity, claims, consents, device registrations, data pointers, and composable domain-specific facets. It works offline, at the edge, in the cloud, across virtual worlds, on smart glasses, in social networks, on blockchains, and in any system that needs to pass verifiable state about an entity between independent parties.

The format is deliberately minimal in its core contract and deliberately expansive in what it can carry. This is what makes it useful: the core is stable and predictable, while the payload (facets, pointers, claims, consents) adapts to any domain without changing the spec.

If a system needs to answer the question "what is true about this entity, right now, in a way that any other system can verify?" -- Universal Manifest is the standard for that answer.
