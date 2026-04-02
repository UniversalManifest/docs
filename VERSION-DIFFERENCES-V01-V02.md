# Version Differences: Universal Manifest v0.1 to v0.2

**Status:** Active  
**Updated:** 2026-04-01  
**Audience:** Implementers, standards reviewers, and platform integrators  
**Normative references:** `spec/v0.1/`, `spec/v0.2/`, `spec/v0.2/SIGNATURE-PROFILE.md`  
**Migration guide:** `docs/guides/MIGRATION-V01-V02.md`

---

## 1. Executive Summary

Universal Manifest v0.2 transforms the specification from a structurally sound but cryptographically permissive document format into a verifiable, trust-layered state capsule. The primary additions are: (1) a normative signature profile using JCS (RFC 8785) canonicalization with Ed25519 signing, making the `signature` field required and interoperable across implementations; (2) an identity binding framework that discloses the "Bag of Claims" vulnerability and introduces a four-tier trust model, an optional `claims[].claimProof` field for Verifiable Presentation evidence, and a non-normative `identity.crossDidBinding` claim convention; and (3) an `um:agentDelegation` pointer convention for delegation transparency in spatial and avatar platforms. The v0.2 changes are designed to be additive wherever possible, preserving the core document shape while closing the most critical security gaps identified through synthetic peer review.

---

## 2. Breaking Changes

v0.2 is designed to be additive to v0.1. However, two changes are breaking for strict consumers and issuers.

| Change | Type | Impact |
|--------|------|--------|
| `manifestVersion` value changes from `"0.1"` to `"0.2"` | Breaking (consumer + issuer) | Consumers with strict version checks reject unknown versions. Issuers must emit the new version string. |
| `signature` field becomes REQUIRED | Breaking (consumer + issuer) | v0.2 consumers MUST reject unsigned manifests. v0.1 issuers that omit `signature` or use the permissive v0.1 format cannot satisfy v0.2 consumers. |
| `signature` shape is constrained to a defined profile | Breaking (consumer) | v0.2 consumers MUST verify JCS + Ed25519 signatures. Consumers that accepted the permissive v0.1 `signature` must add verification logic. |

All other changes (new fields, conventions, security considerations) are additive and non-breaking. The core required fields (`@context`, `@id`, `@type`, `subject`, `issuedAt`, `expiresAt`) remain unchanged. Unknown-field tolerance remains required for forward compatibility.

### Compatibility Notes

| Scenario | Behavior |
|----------|----------|
| v0.1 consumer receives v0.2 manifest | Consumer ignores unknown signature subfields; parses payload structurally but provides no v0.2 trust guarantees. |
| v0.2 consumer receives v0.1 manifest | Rejected in strict v0.2-only policy because signature profile is missing. Dual-version consumers can route by `manifestVersion`. |
| v0.2 issuer sends to v0.1 consumer | Typically accepted due to unknown-field tolerance in v0.1. |

---

## 3. Signature Profile (Major Addition)

v0.2 introduces the first normative, interoperable signature profile. This is the single largest change from v0.1.

### 3.1 Design Rationale

v0.1 declared `signature` as an intentionally permissive placeholder with no defined canonicalization, algorithm, or verification procedure. This meant manifests could not be reliably verified for integrity or authenticity across implementations. v0.2 closes this gap while preserving the local-first design constraint (verification must be feasible on constrained devices such as Android TV and edge boxes).

### 3.2 Profile Selection: JCS + Ed25519

The specification evaluated two approaches:

- **Option A (W3C Data Integrity):** Signs the RDF graph meaning. Higher complexity, more specialized library support required.
- **Option B (JCS + Ed25519):** Signs the JSON representation using deterministic serialization. Broadly implementable without JSON-LD processing.

Option B was selected for v0.2 because it provides the easiest adoption path for third parties and matches the specification's "state capsule" usage where the JSON shape is the primary contract. A W3C Data Integrity profile may be added in a future version.

### 3.3 Signature Shape

The `signature` object MUST contain the following fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `algorithm` | string | Yes | MUST be `"Ed25519"` |
| `canonicalization` | string | Yes | MUST be `"JCS-RFC8785"` |
| `value` | string | Yes | base64url-encoded Ed25519 signature over canonical bytes |
| `keyRef` | string | Conditional | URI reference to verification key material. At least one of `keyRef` or `publicKeySpkiB64` MUST be present. |
| `publicKeySpkiB64` | string | Conditional | base64-encoded SPKI DER public key bytes for offline verification. At least one of `keyRef` or `publicKeySpkiB64` MUST be present. |
| `created` | string (date-time) | No | ISO 8601 timestamp of signature creation (recommended) |
| `statusRef` | string (URI) | No | URI to revocation/status material |
| `revocationCursor` | string | No | Monotonic status cursor for cache-aware revocation checks |

```json
{
  "signature": {
    "algorithm": "Ed25519",
    "canonicalization": "JCS-RFC8785",
    "keyRef": "did:key:z6MkAlice#keys-1",
    "publicKeySpkiB64": "MCowBQYDK2VwAyEA...",
    "created": "2026-04-01T10:00:00Z",
    "value": "base64url-encoded-signature-bytes"
  }
}
```

### 3.4 Signing Input Procedure

1. Start with the complete manifest JSON object.
2. Remove the `signature` property entirely.
3. Canonicalize the remaining object using JCS (RFC 8785), producing a UTF-8 byte sequence.
4. Compute the Ed25519 signature over those bytes.
5. Set the `signature` property on the manifest with the fields defined above.

The `signature` property is excluded from the signing input to avoid circularity. The `statusRef` and `revocationCursor` fields, when present, are metadata for revocation-aware policy checks and do not alter the signing input.

### 3.5 Verifier Checklist

A verifier implementing this profile MUST:

1. Confirm the document is a v0.x Universal Manifest (required fields present, `@type` includes `um:Manifest`).
2. Enforce TTL: reject if `now > expiresAt`; sanity-check `issuedAt <= expiresAt`.
3. Validate the signature profile: require `signature.algorithm === "Ed25519"`, `signature.canonicalization === "JCS-RFC8785"`, and a non-empty `signature.value`.
4. Obtain a public key: if `signature.publicKeySpkiB64` exists, a consumer MAY use it directly (SPKI DER bytes, base64); otherwise, resolve `signature.keyRef` to public key material.
5. Recompute the signing input (remove `signature`, JCS canonicalize).
6. Verify the Ed25519 signature over the canonical bytes.

If verification fails, the manifest MUST be rejected for use (but MAY be retained for debugging).

### 3.6 Profile Identification Semantics

Consumers MUST treat `signature.algorithm` + `signature.canonicalization` as the explicit profile identity.

- If the pair is unsupported, the manifest MUST be rejected when strict verification is required by policy.
- Consumers MUST NOT reinterpret unknown pairs as the baseline profile.

This design enables future profiles (e.g., post-quantum algorithms, alternative canonicalization, or a Data Integrity proof model) to be introduced by defining new algorithm/canonicalization pairs.

### 3.7 Revocation-Aware Verification Extension (Optional)

For consumers claiming revocation-aware verification:

1. If `signature.statusRef` is present, resolve status from that URI (or a configured equivalent).
2. If `signature.revocationCursor` is present, use it to prevent stale-status acceptance and to drive cache revalidation policy.
3. If revocation status cannot be determined and policy requires active status, the manifest MUST be rejected for use.

Consumers that do not implement revocation-aware verification MUST report revocation status as `unchecked` and MUST NOT claim revocation-aware conformance.

### 3.8 What This Means for Implementers

- **Consumers** must add JCS canonicalization and Ed25519 verification to their validation pipeline.
- **Issuers** must provision Ed25519 signing keys, canonicalize unsigned manifests via JCS, and emit the constrained `signature` object.
- **No JSON-LD RDF processing is required.** The v0.2 baseline profile operates at the JSON level.
- **Library availability:** JCS (RFC 8785) and Ed25519 have mature implementations in all major languages.

---

## 4. Identity Binding and Claim Authenticity (Major Addition)

v0.2 introduces a comprehensive identity binding framework, disclosing a structural vulnerability and providing layered mitigations.

### 4.1 The Bag of Claims Vulnerability

A Universal Manifest may contain claims from multiple issuers and references to multiple DIDs under a single `subject`. The v0.2 signature proves that the signer produced the manifest. It does **not** prove:

- That the signer controls the `subject` DID (subject-signer binding).
- That the `subject` controls all DIDs mentioned in claims or facets (cross-DID control).
- That an issuer actually issued a claim listed in the manifest (claim authenticity). The `claims[].issuer` field is a string assertion, not a verified provenance chain.

This means an attacker can copy claims across manifests, fabricate issuer strings, and farm Sybil identities. Five specific attack vectors were identified:

| Attack Vector | Severity |
|---------------|----------|
| Credential stacking (Sybil) | Critical |
| Sybil amplification | Critical |
| Cross-DID identity theft | High |
| Issuer impersonation | High |
| Pairwise DID abuse | Medium |

Relying parties MUST NOT treat the presence of claims in a signed manifest as proof that those claims are authentic or that multiple DIDs are controlled by the same entity.

### 4.2 Four-Tier Trust Model

The specification defines four trust tiers for claim verification. Each tier is strictly additive -- a higher-tier manifest satisfies all lower-tier requirements. The specification does NOT mandate a minimum tier; relying parties choose based on their threat model.

**Tier 0 -- Signature-only.** Zero friction. Claims are self-asserted by the manifest signer. No external evidence of claim authenticity is present. Suitable for low-stakes use cases where the relying party has an out-of-band trust relationship with the signer.

**Tier 1 -- Attested or evidence-backed.** Low friction. Some or all claims carry external evidence of authenticity via `claims[].claimProof` (Verifiable Presentations) or an attested cross-DID binding claim (`identity.crossDidBinding`). Relying parties can verify specific claims against their issuers or evaluate attester trust. Suitable for medium-stakes use cases (social identity, reputation, basic access control).

**Tier 2 -- Cryptographic binding.** Medium friction. Cross-DID control is cryptographically proven via multi-signature binding or zero-knowledge proofs. Each DID independently proves control by signing. Suitable for high-stakes Sybil-resistance use cases. **Deferred to v0.3.**

**Tier 3 -- Multi-party ceremony.** High friction. Multiple keyholders (potentially different people, different locations) must co-sign. Analogous to multi-sig wallets. Suitable for the highest-stakes organizational and financial contexts. **Deferred to v0.4+.**

**Design principle:** Users should never face more friction than their use case requires. Higher tiers provide stronger guarantees but impose more ceremony.

**Relying party requirements:**
- Relying parties MUST define their required trust tier based on their threat model.
- Relying parties MUST NOT extend trust from one DID in a manifest to another DID in the same manifest unless binding evidence (Tier 1 or Tier 2) is present for that specific DID pair.

### 4.3 `claims[].claimProof` Optional Field

*Status: Optional, non-breaking schema addition for v0.2.*

A new optional `claimProof` field on claim objects carries a Verifiable Presentation or attestation proof demonstrating claim issuance to the manifest subject. This field enables Tier 1 verification.

The field is named `claimProof` rather than `evidence` to avoid collision with the W3C Verifiable Credentials Data Model v2.0 `evidence` property (VCDM section 9.2), which has overlapping but distinct semantics.

`claimProof` MAY be:
- An **embedded object** (a VP or attestation proof), or
- A **string** (URI reference to a VP or attestation endpoint).

**Verification rules when `claimProof` is present:**

1. If an embedded VP object, the consumer SHOULD verify the VP proof chain: (a) VC signature validates to the stated issuer, (b) VP signature validates to the holder, (c) holder DID matches the manifest `subject`.
2. If a URI string, the consumer MAY fetch the VP for verification when network access is available. Consumers that cannot resolve the URI SHOULD report the claim as `claimProof-unresolved` rather than `verified`.
3. VPs used as `claimProof` SHOULD include domain (audience binding) and challenge (nonce) parameters to prevent cross-manifest replay.

**Size limits:** Maximum 50 KB per embedded VP. Maximum 500 KB total VP payload across all claims in one manifest. Consumers MUST reject manifests exceeding these limits.

```json
{
  "claims": [
    {
      "@type": "personhood.worldId.verification",
      "issuer": "did:web:worldcoin.org",
      "claimProof": {
        "@type": "um:AttestationEvidence",
        "ref": "https://notary.example/attestations/abc123"
      }
    }
  ]
}
```

### 4.4 `identity.crossDidBinding` Claim Convention

*Status: Non-normative recommendation for v0.2.*

A new claim convention for asserting that multiple DIDs are controlled by the same entity. It works within the existing `claims[]` array and requires no schema changes.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `@type` | string | Yes | MUST be `"identity.crossDidBinding"` |
| `boundDids` | string[] | Yes | DIDs asserted as equivalent. At least 2. One MUST match `subject`. |
| `attester` | string | Yes | DID or URI of the attesting entity |
| `attestationMethod` | string | Yes | Human-readable verification method description |
| `attestedAt` | string (date-time) | Yes | When the attestation was produced |
| `claimProof` | object or string | No | URI or structured object pointing to attestation proof |
| `expiresAt` | string (date-time) | No | Attestation expiry. Relying parties SHOULD reject expired attestations. |

```json
{
  "@type": "identity.crossDidBinding",
  "boundDids": ["did:key:z6MkAlice", "did:plc:alice-bsky"],
  "attester": "did:web:verify.example",
  "attestationMethod": "AT Protocol handle resolution",
  "attestedAt": "2026-03-15T10:30:00Z",
  "expiresAt": "2026-06-15T10:30:00Z"
}
```

**Security notes:**
- Binding strength is trust-delegated, not cryptographic. Only as strong as the attester.
- The attester learns the DID pair -- this has privacy implications (see section 6).
- Relying parties SHOULD maintain a configurable attester trust list.
- Multiple binding claims for overlapping DID sets are independent assertions, not cumulative proof.

### 4.5 `requiredTrustTier` Declaration Convention

*Status: Non-normative convention for v0.2. Expected to become normative in v0.3.*

A manifest MAY declare the minimum trust tier required for specific claims, facets, or the manifest as a whole via a `requiredTrustTier` integer (0-3).

- **Manifest-level:** A top-level `requiredTrustTier` sets the floor for the entire manifest.
- **Claim-level:** A `requiredTrustTier` on an individual claim applies to that claim only.
- **Facet-level:** A `requiredTrustTier` on a facet applies to that facet only.

If a claim carries `requiredTrustTier: 2` but the relying party can only verify at Tier 1, the relying party MUST treat that claim as unverified. If absent, the default is 0. The manifest-level value sets the floor; claim/facet-level values can only raise it, not lower it.

```json
{
  "requiredTrustTier": 1,
  "claims": [
    {
      "@type": "personhood.worldId.verification",
      "issuer": "did:web:worldcoin.org",
      "requiredTrustTier": 2
    }
  ]
}
```

### 4.6 Bilateral Exchange Model

A fundamental architectural principle introduced in v0.2: in any transaction or interaction, both parties present a Universal Manifest to each other. Trust verification is inherently bilateral.

- Alice presents her UM to a venue; the venue verifies Alice's claims at the trust tier the venue requires.
- The venue presents its UM to Alice; Alice verifies the venue's claims at the trust tier Alice requires.
- A peer-to-peer exchange has both sides presenting and verifying simultaneously.

The effective trust tier for an interaction is the maximum of what either party demands. Asymmetric requirements are valid. Two devices MAY exchange manifests via local transport (NFC, BLE, QR) and each independently verify the other's claims at the declared tier without a server.

### 4.7 What This Means for Implementers

- **No immediate code changes required** for the identity binding additions. `claimProof` is optional. The claim conventions use the existing `claims[]` and `pointers[]` arrays.
- **Relying parties** should evaluate which trust tier their use case requires and implement verification logic accordingly.
- **Issuers** should consider whether their claims need attestation evidence (`claimProof`) or cross-DID binding for the relying parties they serve.
- **The upgrade path is incremental:** implementations can start at Tier 0 (signature-only, which is the v0.2 baseline) and add Tier 1 verification as credential providers begin issuing VCs.

---

## 5. Agent Delegation (New Convention)

*Status: Non-normative convention for v0.2.*

### 5.1 Problem

A manifest can contain pointers to a 3D avatar payload or active spatial session, but the manifest is a static document. It cannot prove whether the entity currently controlling a session is the verified human subject or a delegated AI agent. Full liveness verification is a runtime/platform problem, not a document format problem.

### 5.2 `um:agentDelegation` Pointer Convention

v0.2 solves the tractable subset -- **delegation transparency** -- by introducing a pointer convention that declares when a session is operating under delegated authority. The pointer is placed in the manifest's `pointers` array.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `@type` | string | Yes | MUST be `"um:agentDelegation"` |
| `delegateType` | string | Yes | `"ai-agent"`, `"bot"`, `"proxy"`, or `"human-delegate"` |
| `delegatedBy` | string | Yes | DID of the delegating subject. MUST match manifest `subject`. |
| `delegatedAt` | string (date-time) | Yes | When delegation was granted |
| `expiresAt` | string (date-time) | Yes | Delegation expiry. Platforms MUST reject expired delegations. |
| `delegateId` | string | No | DID or identifier of the delegate entity |
| `scope` | string[] | No | Capabilities the delegate may exercise |
| `livenessEndpoint` | string (URI) | No | URI for real-time liveness/delegation status queries |

```json
{
  "@type": "um:agentDelegation",
  "delegateType": "ai-agent",
  "delegateId": "did:key:z6MkAgentBot",
  "delegatedBy": "did:key:z6MkAlice",
  "delegatedAt": "2026-04-01T10:00:00Z",
  "expiresAt": "2026-04-01T11:00:00Z",
  "scope": ["spatial.session", "social.messaging"]
}
```

### 5.3 Platform Guidance

- Platforms SHOULD display delegation status to other users when present (e.g., "Alice (via AI agent)").
- Platforms MAY require human-only sessions for high-stakes actions (financial, governance).
- Platforms MAY query `livenessEndpoint` for real-time status when available.
- Platforms MUST treat the delegation pointer as static for the manifest's TTL if `livenessEndpoint` is absent.

### 5.4 What This Means for Spatial/Avatar Platforms

The delegation pointer preserves the local-first design: the delegation fact is part of the signed manifest and verifiable offline. The optional `livenessEndpoint` adds real-time capability for platforms that need it. Full human liveness verification (biometric challenges, interaction analysis) remains a platform responsibility, not a manifest property.

---

## 6. Privacy Enhancements

### 6.1 Privacy-Binding Tension Framework

v0.2 introduces explicit guidance on the fundamental tension between privacy-preserving pairwise DIDs and cross-DID binding mechanisms. Stronger binding enables correlation, while stronger privacy prevents binding verification.

The specification does not resolve this tension at the protocol level. Instead, it provides mechanisms for both and establishes normative guardrails:

- Relying parties MUST NOT require cross-DID binding unless their use case demands Sybil resistance or trust transitivity.
- Subjects SHOULD use the minimum binding tier that satisfies their relying parties' requirements.

### 6.2 Pairwise DID Interaction per Trust Tier

| Trust Tier | Pairwise DID Privacy | Binding Impact |
|------------|---------------------|----------------|
| Tier 0 | Fully preserved | No cross-DID linking |
| Tier 1 (attested binding) | Partially compromised | The attester learns the DID pair; relying parties may learn linked DIDs |
| Tier 2 (cryptographic, future) | Configurable | ZK proofs can preserve privacy; multi-sig exposes linkage |
| Tier 3 (ceremony, future) | Reduced | Multi-party signing inherently reveals participant identity |

### 6.3 Data Protection Scope Note

The privacy considerations in the specification identify relevant data protection provisions but do not constitute a Data Protection Impact Assessment (DPIA). Deployers operating under GDPR or equivalent frameworks MUST conduct their own assessment, particularly for:

- Cross-DID binding attestation services (potential DPIA trigger under Article 35)
- Cross-border attester data flows (Chapter V transfer requirements)
- Mandatory binding requirements that may undermine freely-given consent (Article 7(4))

---

## 7. Security Enhancements

### 7.1 Extended Threat Model

v0.2 extends the threat model with five new attack vectors specific to the Bag of Claims vulnerability:

| Attack Vector | Severity | v0.2 Response |
|---------------|----------|---------------|
| Credential stacking (Sybil) | Critical | `claimProof` field upgrade path + consumer guidance |
| Sybil amplification | Critical | Combined L1 guidance + consumer guidance |
| Cross-DID identity theft | High | Attested binding + trust transitivity warning |
| Issuer impersonation | High | `claimProof` field upgrade path + security disclosure |
| Pairwise DID abuse | Medium | Privacy-binding tension documentation |

Additionally, the signature profile addresses:

| Threat | Mitigation |
|--------|------------|
| Replay attacks | TTL enforcement (carried from v0.1, now reinforced) |
| Tampering | Ed25519 signature verification |
| Key compromise | Key rotation and revocation infrastructure guidance |
| Revocation bypass | Revocation-aware verification extension |
| DoS attacks | Resource limits (carried from v0.1: 1 MB size, 10 levels depth, 1,000 array elements) |
| Signature stripping | Mandatory signature requirement in v0.2 |
| Downgrade attacks | Profile validation (reject unsupported algorithm/canonicalization pairs) |

### 7.2 Resource Limits and DoS Protections

v0.2 adds VP-specific size limits on top of the v0.1 resource limits:

| Limit | Value | Version Introduced |
|-------|-------|--------------------|
| Maximum total JSON size | 1 MB | v0.1 |
| Maximum JSON nesting depth | 10 levels | v0.1 |
| Maximum array sizes | 1,000 elements | v0.1 |
| Maximum embedded VP size | 50 KB per VP | v0.2 |
| Maximum total VP payload | 500 KB across all claims | v0.2 |

### 7.3 Key Rotation and Revocation Guidance

v0.2 introduces operational guidance for signing key management:

- Rotate signing keys on schedule (30-90 days for high-volume issuers) or immediately on suspected compromise.
- Publish public keys at stable `signature.keyRef` URLs.
- Maintain revocation infrastructure (`signature.statusRef` endpoints).
- Respond to key compromise incidents within 24 hours.
- Keep previous public keys available for a grace period aligned with manifest TTL and audit requirements.

---

## 8. Schema Changes Summary

### 8.1 Field-by-Field Comparison

| Field / Path | v0.1 | v0.2 | Change Type |
|-------------|------|------|-------------|
| `manifestVersion` | `type: string` (any value) | `const: "0.2"` | Breaking: value constrained |
| `signature` | Optional, permissive object (`$defs/signature`) | **Required**, constrained profile (`$defs/signatureV02`) | Breaking: now required with defined shape |
| `signature.algorithm` | `type: string` (any) | `const: "Ed25519"` | Breaking: value constrained |
| `signature.canonicalization` | Not defined | `const: "JCS-RFC8785"` | New required field |
| `signature.value` | `type: string` (optional) | `type: string, minLength: 1` (required) | Now required |
| `signature.keyRef` | `type: string` (optional) | `type: string, minLength: 1` (conditionally required) | Conditional: at least one of `keyRef` or `publicKeySpkiB64` must be present |
| `signature.publicKeySpkiB64` | Not defined | `type: string, minLength: 1` (conditionally required) | New field |
| `signature.created` | Not defined | `type: string, format: date-time` (optional) | New optional field |
| `signature.statusRef` | Not defined | Allowed via `additionalProperties` | New optional field (non-schema) |
| `signature.revocationCursor` | Not defined | Allowed via `additionalProperties` | New optional field (non-schema) |
| `claims[].claimProof` | Not defined | `oneOf: [object, string(uri)]` (optional) | New optional field |
| `requiredTrustTier` | Not defined | integer 0-3 (convention, not in schema) | Non-normative convention |
| All other fields | Unchanged | Unchanged | No change |

### 8.2 Schema `$defs` Comparison

**v0.1 `$defs/signature`:**
```json
{
  "type": "object",
  "description": "Permissive v0.1 signature (format not locked yet).",
  "properties": {
    "algorithm": { "type": "string" },
    "keyRef": { "type": "string" },
    "value": { "type": "string" }
  },
  "additionalProperties": true
}
```

**v0.2 `$defs/signatureV02`:**
```json
{
  "type": "object",
  "description": "v0.2 interoperable signature profile (JCS + Ed25519).",
  "required": ["algorithm", "canonicalization", "value"],
  "properties": {
    "algorithm": { "const": "Ed25519" },
    "canonicalization": { "const": "JCS-RFC8785" },
    "keyRef": { "type": "string", "minLength": 1 },
    "publicKeySpkiB64": { "type": "string", "minLength": 1 },
    "created": { "type": "string", "format": "date-time" },
    "value": { "type": "string", "minLength": 1 }
  },
  "anyOf": [
    { "required": ["keyRef"] },
    { "required": ["publicKeySpkiB64"] }
  ],
  "additionalProperties": true
}
```

### 8.3 Top-Level `required` Array Comparison

| v0.1 | v0.2 |
|------|------|
| `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt` | `@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`, **`signature`** |

---

## 9. Related Standards Alignment (New)

v0.2 explicitly cites and positions itself relative to the following standards. These references are new in v0.2; v0.1 did not include a formal references section.

| Standard | Relevance to v0.2 |
|----------|--------------------|
| **RFC 8785 (JCS)** | Canonicalization step in the v0.2 signature profile. |
| **NIST SP 800-63-3** | Identity Assurance Levels (IAL 1-3). The UM tiered trust model adapts NIST's tiered assurance framework to a local-first, portable document context. |
| **eIDAS 2.0** (EU 2024/1183) | Assurance levels (Low, Substantial, High) for electronic identification. Relevant for GDPR alignment. UM tiers map approximately: Tier 0 below Low, Tier 1 ~ Low/Substantial, Tier 2 ~ Substantial/High, Tier 3 ~ High. |
| **OpenID for Verifiable Presentations (OID4VP)** | VP presentation with audience binding and nonce parameters. The `claims[].claimProof` VP recommendations (domain + challenge) align with OID4VP patterns. |
| **DIF Presentation Exchange 2.0** | How relying parties express credential/claim requirements. `requiredTrustTier` is a simplified analog. |
| **DIF Well-Known DID Configuration** v0.2 | Prior art for cross-DID linking via domain linkage credentials. `identity.crossDidBinding` is analogous but manifest-embedded rather than domain-hosted. |
| **RFC 9449 (DPoP)** | Proof-of-possession binding for OAuth2 tokens. Directly analogous to the subject-signer binding problem addressed by the tiered trust model. |
| **W3C VC Status List** / Bitstring Status List v1.0 | Privacy-preserving credential revocation and freshness checking. Target mechanism for `claims[].claimProof` credential status verification. |
| **W3C Verifiable Credentials Data Model v2.0** | Core VC/VP data model. `claims[].claimProof` is inspired by but distinct from VCDM's `evidence` property (Section 9.2). |
| **ISO/IEC 29115** | Entity authentication assurance levels (LoA 1-4). Additional prior art for the tiered trust model. |

---

## 10. Migration Checklist

### MUST (Required for v0.2 Conformance)

- [ ] Update `manifestVersion` from `"0.1"` to `"0.2"` in issued manifests.
- [ ] **Issuers:** Provision an Ed25519 signing key pair.
- [ ] **Issuers:** Implement JCS (RFC 8785) canonicalization of the manifest (with `signature` removed).
- [ ] **Issuers:** Compute Ed25519 signature over canonical bytes and emit the constrained `signature` object with `algorithm`, `canonicalization`, `value`, and at least one of `keyRef` or `publicKeySpkiB64`.
- [ ] **Consumers:** Add JCS canonicalization and Ed25519 signature verification to the validation pipeline.
- [ ] **Consumers:** Reject manifests with missing or invalid signatures.
- [ ] **Consumers:** Validate `signature.algorithm === "Ed25519"` and `signature.canonicalization === "JCS-RFC8785"`.
- [ ] **Consumers:** Reject unsupported signature algorithm/canonicalization pairs (prevent downgrade attacks).
- [ ] **Consumers:** Continue enforcing TTL (`now > expiresAt` rejection) and resource limits.

### SHOULD (Recommended)

- [ ] **Issuers:** Publish public keys at stable `signature.keyRef` URLs.
- [ ] **Issuers:** Include `signature.created` timestamp.
- [ ] **Issuers:** Implement key rotation policy (30-90 days recommended).
- [ ] **Consumers:** Implement version-aware validation (dual v0.1/v0.2 support during transition).
- [ ] **Consumers:** Define and enforce a trust tier requirement for your use case.
- [ ] **Consumers:** Maintain a configurable attester trust list if evaluating `identity.crossDidBinding` claims.
- [ ] **Both:** Plan a v0.1 sunset date and emit telemetry to measure v0.1 retirement readiness.

### MAY (Optional Adoption)

- [ ] **Issuers:** Add `claims[].claimProof` to claims that have VP or attestation evidence.
- [ ] **Issuers:** Include `identity.crossDidBinding` claims for cross-DID binding assertions.
- [ ] **Issuers:** Include `um:agentDelegation` pointers for delegation transparency.
- [ ] **Issuers:** Declare `requiredTrustTier` on manifests, claims, or facets.
- [ ] **Issuers:** Set up revocation infrastructure (`signature.statusRef`, `signature.revocationCursor`).
- [ ] **Consumers:** Implement revocation-aware verification.
- [ ] **Consumers:** Verify `claims[].claimProof` VP proof chains when present.
- [ ] **Consumers:** Process `requiredTrustTier` declarations and enforce minimum tier requirements.
- [ ] **Platforms:** Display `um:agentDelegation` status to users.
- [ ] **Platforms:** Query `livenessEndpoint` for real-time delegation status when available.

### Reference Documents

- Full migration guide: `docs/guides/MIGRATION-V01-V02.md`
- v0.2 signature profile: `spec/v0.2/SIGNATURE-PROFILE.md`
- v0.2 schema: `spec/v0.2/schema.json`
- Identity binding proposal: `.dev/ai/proposals/PROPOSAL-v0.2-identity-binding-and-liveness.md`
- W3C-style specification: `docs/W3C-STYLE-SPEC.html`
- Threat model: `docs/security/THREAT-MODEL.md`
- Deprecation policy: `docs/governance/DEPRECATION-POLICY.md`
