# Portable Identity Profile Implementation and Gap Assessment for Universal Manifest

Date: 2026-03-05  
Project: Universal Manifest (`/Users/grig/work/repo/universalmanifest`)

## Scope

This report evaluates the "Portable Identity Profile" requirements against the current Universal Manifest (UM) system and answers three questions for each requirement:

1. Is it already supported?
2. If not fully supported, where is the gap?
3. How should it be implemented, with a concrete example?

Assessment labels used:

- `Covered`: directly supported by current UM spec + docs + fixtures.
- `Partial`: implementable now, but key behavior is non-normative, optional, or missing standardization.
- `Gap`: not currently standardized in UM and needs new profile/spec work.

## Executive Verdict

UM already provides a strong foundation for Portable Identity Profile:

- portable cross-system identity/state envelope,
- consent model,
- pointer-based composition,
- TTL freshness,
- v0.2 signature verification,
- revocation-aware extension lane,
- XR/metaverse/smart-glasses integration lanes.

Main gaps for a production-grade Portable Identity Profile standard are concentrated in five areas:

1. encrypted private-fragment standardization,
2. selective disclosure / ZK proof profile,
3. wallet recovery profile,
4. wallet transport/profile interoperability conventions (OIDC4VP/OIDC4VCI/DIDComm binding guidance),
5. tighter registry/governance for XR-specific field naming.

These are evolvable gaps, not architectural blockers.

## Requirement-by-Requirement Assessment

### 1) Cross-device, cross-app interoperability (PC, AR phone/eyewear, VR/MR headset, native, streamed, WebXR)

- Status: `Covered`
- Current UM support:
  - UM is explicitly spec-first and language/runtime neutral.
  - JSON-LD + JSON shape with unknown-field tolerance supports broad consumer diversity.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/README.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
- Implementation now:
  - Build one issuer pipeline and multiple consumer projections.
  - Enforce baseline parse + TTL + unknown-field tolerance on every surface.
- Applied example:
  - A headset app reads `metaverse.avatar` pointer and `crossWorldProfile` shard for full immersive render.
  - A phone AR app only reads `ar.profile.public` pointer and `ar.overlay.presenceVisible` consent for lightweight overlay.

### 2) User ownership/control of data and identity security

- Status: `Partial`
- Current UM support:
  - Supports DID-based subjects, short TTL, signature verification (v0.2), consent gating.
  - Supports pointer-based decentralized data placement.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md`
- Gap:
  - "Ownership/control" is supported architecturally, but not enforced as a strict conformance profile (for example, no mandatory wallet control semantics).
- Implementation now:
  - Use wallet-controlled keys for signing and per-surface consent decisions.
  - Store large assets off-manifest and reference by pointers.
- Applied example:
  - `subject: did:key:...`, signed manifest (`Ed25519`), consent `social.profilePublic=denied`, pointers to user-controlled storage endpoints.

### 3) Privacy-by-default with public minimal profile + encrypted private fragments

- Status: `Partial` (with a core gap)
- Current UM support:
  - Default-deny consent model is already established in integrations.
  - Minimal disclosure principle is already documented.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/integrations/data-firewall-ux.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md`
- Gap:
  - No standardized encrypted-fragment/shard profile in UM core today.
- Implementation now:
  - Keep private data out of manifest body; use protected pointers and wallet-mediated retrieval.
  - Treat manifest as minimal public control plane plus references.
- Change recommended:
  - Add a non-normative "Encrypted Fragment Profile" first, then standardize if adopter convergence appears.
- Applied example:
  - Public shard: `publicProfile` with non-sensitive fields.
  - Private pointer: `wallet.privateBundle` -> encrypted object retrievable only after wallet authorization.

### 4) Pseudonymity and pairwise IDs to prevent cross-service correlation

- Status: `Partial`
- Current UM support:
  - Pairwise/pseudonymous DID usage is explicitly recommended.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md`
- Gap:
  - Recommendation exists, but not a conformance requirement with test fixtures.
- Implementation now:
  - Issue different subject DIDs for different relying parties and rotate `@id` per issuance.
- Change recommended:
  - Add extended privacy conformance fixtures proving pairwise DID behavior.
- Applied example:
  - For same human:
    - retail realm subject: `did:web:retail.example:users:abc`
    - game realm subject: `did:web:game.example:users:xyz`
  - Both map to user wallet internally, but cannot be correlated by default.

### 5) Selective disclosure / ZK proofs (BBS+, CL, SD-JWT, etc.)

- Status: `Gap`
- Current UM support:
  - UM can carry proof references and minimally disclosed claims.
  - Security docs explicitly call ZK/selective disclosure a future extension layer.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/docs/security/THREAT-MODEL.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/README.md`
- Gap:
  - No normative UM selective-disclosure proof profile yet.
- Implementation now:
  - Use pointers to external VP/VC proofs and include only decision-grade outputs in claims.
- Change recommended:
  - Define a "Proof-Carrying Claim Profile" for UM (proof type, verifier expectations, trust model).
- Applied example:
  - Claim in manifest: `"age.over18": true`
  - Pointer: `"proof.ageOver18": "https://wallet.example/proofs/sd-jwt/abc123"`
  - XR retail checks boolean + verifies proof pointer per policy.

### 6) Data pointers, not copies, for large assets (avatars, wearables, meshes, NFTs)

- Status: `Covered`
- Current UM support:
  - Pointer-first composition is an established UM pattern.
  - Metaverse/XR lanes already use avatar/profile/inventory pointer names.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`
- Implementation now:
  - Keep high-volume binary assets outside manifest, referenced by URLs/CIDs.
- Applied example:
  - Pointers:
    - `metaverse.avatar` -> avatar asset endpoint
    - `metaverse.inventory` -> inventory endpoint
    - `metaverse.socialGraph` -> graph endpoint

### 7) User control and consent prompts/logging

- Status: `Partial`
- Current UM support:
  - Consent keys and default-deny behavior are present.
  - Firewall-style audit logging guidance exists (manifest ID + rule ID).
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/smart-glasses.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/data-firewall-ux.md`
- Gap:
  - Prompt UX and consent-log schema are not standardized as normative UM protocol behavior.
- Implementation now:
  - Wallet prompts user before disclosure; relying parties log decisions keyed by manifest ID.
- Change recommended:
  - Publish a wallet-interop profile for request/decision/audit payload shape.
- Applied example:
  - XR app requests `ar.recording.voiceAllowed`.
  - Wallet prompt appears -> user denies.
  - Decision logged as:
    - `manifestId`, `ruleId`, `consumerId`, `decision=denied`, `timestamp`.

### 8) Recoverability (seed/social/hardware recovery for DID/wallet + manifest access)

- Status: `Gap`
- Current UM support:
  - Recovery is acknowledged as future/out-of-scope in current baseline posture.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/README.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DECISIONS.md`
- Gap:
  - No UM recovery profile or interoperability guidance for wallet/key restoration.
- Implementation now:
  - Handle recovery in wallet ecosystem layer, not UM core.
- Change recommended:
  - Add non-normative "Recovery Integration Lane" and optional recovery metadata conventions.
- Applied example:
  - Pointer: `wallet.recovery.policy` -> recovery descriptor endpoint.
  - Consumer ignores this pointer unless it participates in recovery workflows.

### 9) Revocation and freshness

- Status: `Partial` (strong)
- Current UM support:
  - Freshness (TTL) is mandatory baseline behavior.
  - Revocation-aware verification is explicitly defined as v0.2 extended behavior via `statusRef` and `revocationCursor`.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/CONFORMANCE.md`
  - `/Users/grig/work/repo/universalmanifest/spec/v0.2/SIGNATURE-PROFILE.md`
- Gap:
  - Revocation remains optional unless consumers claim revocation-aware conformance.
- Implementation now:
  - For XR trust-sensitive surfaces, require `v0.2-extended` verification policy.
- Applied example:
  - Manifest includes:
    - `signature.statusRef: https://issuer.example/revocations/umid/123`
    - `signature.revocationCursor: "2026-03-05T11:00:00Z#42"`
  - Consumer rejects on revoked status or stale cursor.

### 10) Three-layer architecture (Wallet/Client, Manifest, Ecosystem protocols)

- Status: `Partial`
- Current UM support:
  - UM clearly occupies manifest/document layer.
  - Adjacent standards are explicitly positioned as complementary (DIDComm, OIDC, VC).
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/docs/STANDARDS-POSITIONING.md`
  - `/Users/grig/work/repo/universalmanifest/docs/DOMAIN-ARCHITECTURE.md`
- Gap:
  - No single normative protocol binding document for wallet handshake flows (QR/deep-link/OIDC4VP/DIDComm).
- Implementation now:
  - Keep UM as payload contract; use existing wallet protocols for transport/presentation.
- Change recommended:
  - Publish a "Wallet Interop Profile for UM" (non-normative first) that maps request/response patterns to UM claims/consents/pointers.
- Applied example:
  - Verifier sends OIDC4VP request for age + consent.
  - Wallet returns VP and UM reference/payload.
  - Relying party enforces UM TTL + consent + proof checks.

### 11) Ecosystem naming conventions and required inclusions

- Status: `Partial`
- Current UM support:
  - v0.1 well-known registry exists.
  - Integration lanes define domain-specific suggested names.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/spec/v0.1/REGISTRY.md`
  - `/Users/grig/work/repo/universalmanifest/integrations/TEMPLATE.md`
  - `/Users/grig/work/repo/universalmanifest/docs/guides/integration-authoring-guide.md`
- Gap:
  - Registry is non-normative and not yet comprehensive for all XR Portable Identity Profile needs.
- Implementation now:
  - Use existing naming conventions (`domain.key`) and keep unknown-field tolerance.
- Change recommended:
  - Add an "XR Portable Identity Profile Registry Pack" with stable keys for avatar, wearables, skeleton mapping, locomotion/privacy preferences.
- Applied example:
  - Suggested key set:
    - `metaverse.avatar`
    - `metaverse.wearables`
    - `xr.avatarSkeleton`
    - `xr.inputProfile`

### 12) Avatar Translation Framework support (metadata + links for transform into internal avatar templates)

- Status: `Partial`
- Current UM support:
  - Metaverse integration lane already models avatar/inventory/profile pointers and cross-world profile shards.
- Evidence:
  - `/Users/grig/work/repo/universalmanifest/integrations/metaverse.md`
  - `/Users/grig/work/repo/universalmanifest/examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`
- Gap:
  - No standardized schema for avatar rig metadata and translation capability descriptors.
- Implementation now:
  - Carry translation metadata in optional shards and provide avatar asset pointers.
- Change recommended:
  - Add an XR translation shard profile (bone map, morph target support, scale constraints, fallback rules).
- Applied example:
  - Shard `avatarTranslationProfile` contains:
    - source format (`vrm`/`gltf`),
    - skeleton profile version,
    - supported blendshape set,
    - target-engine mapping hints.
  - Pointer `metaverse.avatar` gives source asset URI.

## Recommended Implementation Plan

### Phase 1: Immediate deployment using current UM (no spec change)

- Enforce `v0.2-baseline` everywhere and `v0.2-extended` for high-trust XR surfaces.
- Use pointer-first asset references and default-deny consents.
- Use pairwise DIDs operationally even though not mandatory.
- Keep private/sensitive payloads off-manifest unless explicitly needed.

### Phase 2: Near-term hardening (non-normative additions first)

- Publish `Portable Identity Profile XR Integration Lane` under `integrations/`.
- Add fixture set for:
  - avatar translation metadata,
  - wallet-mediated consent audits,
  - pairwise DID operational patterns.
- Publish wallet protocol binding guidance (OIDC4VP/OIDC4VCI/DIDComm transport examples carrying UM payloads/references).

### Phase 3: Normative evolution candidates (v0.3+ consideration)

- Encrypted private-fragment profile.
- Selective disclosure / ZK proof profile.
- Recovery profile conventions.
- XR naming registry governance and graduation criteria from non-normative to normative.

## Final Conclusion

Portable Identity Profile is already highly compatible with UM's architecture and can be implemented now in a production-reasonable form. The core design does not need replacement. It needs targeted profile expansion and registry hardening to fully standardize privacy-preserving and wallet-centric behaviors that your Portable Identity Profile model calls for.
