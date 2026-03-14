# Metaverse Universal Manifest (MUM) Implementation and Gap Assessment for Universal Manifest

Date: 2026-03-05  
Project: Universal Manifest (``)  
Primary source input: `/Users/grig/Desktop/Use Case_ Metaverse Universal Manifest - v1.0.md`

## Scope

This report evaluates the MUM v1.0 use-case requirements against the current Universal Manifest system and answers three questions for each requirement class:

1. Is it already supported?
2. If not fully supported, where is the gap?
3. How should it be implemented now, with a concrete example?

Assessment labels used:

- `Covered`: directly supported by current UM spec + docs + fixtures/journeys.
- `Partial`: feasible now, but key behavior is non-normative, optional, or underspecified for broad interoperability.
- `Gap`: no clear UM profile/guidance exists yet; requires research and/or new profile work.

## Executive verdict

The MUM use case is implementable today with UM as the carrier contract. Existing UM capabilities already cover the core mechanics:

- cross-platform portability,
- identity and claims transport,
- consent gating,
- pointer-based external references,
- TTL freshness controls,
- v0.2 signature integrity and optional revocation-aware posture.

The biggest remaining work is not core feasibility but standardization depth for metaverse-specific operational details:

1. version/synchronization profile and conflict resolution,
2. security hardening profile (anti-cloning, attestation, secure enclave semantics),
3. selective disclosure/compliance proof profile,
4. deeper registry conventions for scenario-5 preference classes,
5. accountability semantics for platform-local copies and downstream handling.

Conclusion: this is a `build-now with targeted hardening` situation, not an architectural blocker.

## Requirement-by-requirement assessment

### 1) Cross-platform interoperability and portability across metaverse systems

- Status: `Covered`
- Current UM support:
  - JSON-LD + unknown-field tolerance supports heterogenous consumers.
  - Integration lane exists for metaverse projection.
- Evidence:
  - `spec/v0.1/README.md`
  - `spec/v0.1/CONFORMANCE.md`
  - `integrations/metaverse.md`
  - `docs/journeys/journey-09-metaverse-crossworld-projection.md`
- Implementation now:
  - Keep platform-specific semantics in optional facets/pointers/consents.
- Applied example:
  - Platform A resolves `metaverse.avatar` and `metaverse.profile`.
  - Platform B ignores unsupported facet fields and still validates base manifest.

### 2) DID/VC-based identity and credential portability

- Status: `Covered`
- Current UM support:
  - DID subject identifiers are recommended.
  - VC-style claims can be carried as claim payloads and/or facet references.
- Evidence:
  - `spec/v0.1/README.md`
  - `docs/STANDARDS-POSITIONING.md`
- Implementation now:
  - Use DID in `subject`, carry verifier-relevant credential references in pointers/claims.
- Applied example:
  - `subject: did:web:user.example:abc`
  - Claim `verification.status=verified`
  - Pointer `compliance.kycProof -> https://issuer.example/proofs/123`

### 3) Avatar, inventory, NFT, and asset metadata portability

- Status: `Covered`
- Current UM support:
  - Pointer-first composition explicitly supports externalized assets.
  - Metaverse lane defines suggested pointer names for profile/avatar/inventory/social/reputation.
- Evidence:
  - `integrations/metaverse.md`
  - `spec/v0.1/REGISTRY.md`
  - `examples/v0.1/stubs/metaverse-crossworld-profile-manifest.jsonld`
- Implementation now:
  - Keep large asset data off-manifest; keep only references and minimal metadata in facets.
- Applied example:
  - `metaverse.avatar -> ipfs://...`
  - `metaverse.inventory -> https://wallet.example/inventory`

### 4) Persistent social graph and reputation continuity

- Status: `Partial`
- Current UM support:
  - Pointer fields for social graph and reputation are modeled in metaverse lane guidance.
- Gap:
  - No normative profile for social graph schema, trust provenance, or portability semantics across worlds.
- Evidence:
  - `integrations/metaverse.md`
  - `docs/journeys/journey-09-metaverse-crossworld-projection.md`
- Implementation now:
  - Use pointer contracts + explicit consent controls for sharing scope.
- Change recommended:
  - Publish a non-normative social/reputation profile first, then promote as convergence appears.
- Applied example:
  - `metaverse.socialGraph` pointer + consent `metaverse.socialGraphShare=restricted`.

### 5) Privacy and consent propagation across platforms

- Status: `Partial`
- Current UM support:
  - Consent entries already model allow/deny/restricted behavior.
  - Smart-glasses lane demonstrates consent-enforced behavior in context.
- Gap:
  - Cross-platform propagation semantics and update SLAs are not standardized.
- Evidence:
  - `spec/v0.1/REGISTRY.md`
  - `integrations/smart-glasses.md`
  - `docs/journeys/journey-08-smart-glasses-consent-enforcement.md`
- Implementation now:
  - Treat manifest refresh cycle + TTL expiration as propagation driver.
- Change recommended:
  - Define a synchronization profile (change-log pointers, staleness rules, replay-safe update model).
- Applied example:
  - User revokes `metaverse.voiceCapture`; platform checks freshness and updates policy before next session start.

### 6) Secure/compliant transaction flow (KYC/AML, identity checks)

- Status: `Partial`
- Current UM support:
  - UM can carry compliance status claims and proof pointers.
  - v0.2 signature + revocation extension lane supports integrity and status posture.
- Gap:
  - No canonical compliance claim taxonomy and no selective disclosure profile in UM core.
- Evidence:
  - `spec/v0.2/SIGNATURE-PROFILE.md`
  - `spec/v0.2/CONFORMANCE.md`
  - `docs/security/THREAT-MODEL.md`
- Implementation now:
  - Carry decision-grade compliance flags + proof references.
- Change recommended:
  - Add proof-carrying compliance profile with verifier expectations.
- Applied example:
  - `claim: compliance.kycStatus=pass`
  - `pointer: compliance.kycProof=https://issuer.example/vp/abc`

### 7) Scenario-5 preference bundle (language, financial, logistics, voice, security, credentials)

- Status: `Partial`
- Current UM support:
  - UM supports arbitrary namespaced claims/consents/pointers/facets.
- Gap:
  - No registry pack yet for these exact preference classes and context policy semantics.
- Evidence:
  - `spec/v0.1/REGISTRY.md`
  - `spec/v0.1/CONFORMANCE.md`
- Implementation now:
  - Use namespaced key families in optional sections.
- Change recommended:
  - Publish MUM preference registry pack as non-normative guidance.
- Applied example:
  - `prefs.language.default=en-US`
  - `prefs.financial.defaultCurrency=USD`
  - `prefs.logistics.defaultAddressRef=https://vault.example/address/home`
  - `consent.voice.translation=true`
  - `security.auth.workplace=mfa`

### 8) Manifest versioning, staleness detection, and synchronized updates

- Status: `Partial`
- Current UM support:
  - Timestamps (`issuedAt`, `expiresAt`) and TTL enforcement are defined.
  - v0.2 revocation cursor pattern offers a model for freshness-aware status handling.
- Gap:
  - No explicit UM version-sync protocol for authoritative source comparison and conflict resolution.
- Evidence:
  - `spec/v0.1/CONFORMANCE.md`
  - `spec/v0.2/SIGNATURE-PROFILE.md`
  - `docs/journeys/journey-02-ttl-and-freshness.md`
- Implementation now:
  - Use TTL + rotated manifest issuance + authoritative pointer.
- Change recommended:
  - Add synchronization profile (authoritative source pointer, change-log pointer, conflict handling guidance).
- Applied example:
  - Platform compares cached `issuedAt` vs authoritative manifest metadata; stale cache triggers pull.

### 9) Platform integration options (direct use, local copy, API integration, append-only logs)

- Status: `Partial`
- Current UM support:
  - UM is transport and storage neutral; pointer model supports many integration styles.
- Gap:
  - Accountability and copy-control semantics for local copies are not standardized.
- Evidence:
  - `spec/v0.1/README.md`
  - `docs/security/THREAT-MODEL.md`
- Implementation now:
  - Permit local copies only under explicit TTL and consent policy; log access decisions.
- Change recommended:
  - Define platform-handling profile for copy lifecycle, retention, and auditability.
- Applied example:
  - Local cache allowed for 10 minutes; post-expiry requires re-resolution and policy re-check.

### 10) User control options (authentication choice, storage choice, granular permissions)

- Status: `Covered`
- Current UM support:
  - UM is storage-neutral and method-neutral.
  - Granular consent model exists through named consent keys.
- Evidence:
  - `spec/v0.1/README.md`
  - `spec/v0.1/REGISTRY.md`
- Implementation now:
  - Encode user-selected controls as claims/consents/pointers without forcing one wallet/storage provider.
- Applied example:
  - User maintains self-hosted profile pointer while allowing platform-managed cached projection under scoped consent.

### 11) Security hardening requirements (audit trails, anti-cloning, secure enclave, platform attestation)

- Status: `Gap`
- Current UM support:
  - Strong integrity posture in v0.2, plus threat model guidance.
- Gap:
  - No standardized anti-cloning holder-binding profile.
  - No standard platform attestation or secure enclave metadata profile in UM.
- Evidence:
  - `spec/v0.2/SIGNATURE-PROFILE.md`
  - `docs/security/THREAT-MODEL.md`
- Implementation now:
  - Use short TTL + signature verification + optional revocation status checks + external attestation channels.
- Change recommended:
  - Create MUM security profile track for holder binding and attested requester posture.
- Applied example:
  - Platform access request includes attestation evidence pointer; wallet denies high-risk requests lacking attestation.

### 12) Selective disclosure and minimal data exposure

- Status: `Gap`
- Current UM support:
  - Minimal-disclosure guidance exists; proof pointers are feasible.
- Gap:
  - No normative selective-disclosure profile (SD-JWT VC/BBS+/ZK binding rules).
- Evidence:
  - `docs/security/THREAT-MODEL.md`
  - `spec/v0.2/README.md`
- Implementation now:
  - Reference external proof artifacts and expose only decision-grade booleans in manifest claims.
- Change recommended:
  - Standardize a selective disclosure profile for metaverse compliance/age/eligibility checks.
- Applied example:
  - `claim age.over18=true` + `proof.ageOver18` pointer; consumer verifies proof without exposing full credential.

### 13) Legacy/non-compatible platform handling

- Status: `Covered`
- Current UM support:
  - Unknown-field tolerance and optional overlays make progressive integration viable.
- Evidence:
  - `spec/v0.1/CONFORMANCE.md`
  - `integrations/TEMPLATE.md`
- Implementation now:
  - Provide minimal baseline manifest path for legacy consumers; require manual onboarding when unsupported.
- Applied example:
  - Legacy world only reads base identity + TTL-valid consent flags, ignores advanced facets.

### 14) Standards alignment expectations (MSF/OMA3/W3C/DIF/Khronos/VRM)

- Status: `Partial`
- Current UM support:
  - UM is positioned on W3C + IETF standards and explicitly acknowledges MUM lineage.
  - Active integration lanes exist for OMA3 ecosystem context.
- Gap:
  - No formal crosswalk document for each listed SPP/POG requirement from the MUM use case.
- Evidence:
  - `docs/STANDARDS-POSITIONING.md`
  - `docs/MSF-RELATIONSHIP.md`
  - `integrations/metaverse.md`
- Implementation now:
  - Maintain standards-neutral carrier model and adapter-style integration lanes.
- Change recommended:
  - Publish explicit MUM standards crosswalk matrix as non-normative report.
- Applied example:
  - VRM and glTF references remain in metaverse translation facet profile without changing core UM required fields.

## Consolidated gap set (priority order)

Priority 1 (immediate planning):

1. MUM synchronization/versioning profile (staleness + conflict handling).
2. MUM preference registry pack for scenario-5 keys.
3. MUM security handling profile (copy lifecycle + audit semantics).

Priority 2 (research-first hardening):

4. Selective disclosure/compliance proof profile.
5. Anti-cloning and holder-binding profile.
6. Platform attestation and secure enclave interoperability profile.

Priority 3 (governance and ecosystem clarity):

7. MUM standards crosswalk and external-alignment evidence pack.
8. Social/reputation schema portability profile.

## Practical doability conclusion

All major MUM scenarios can be implemented now on UM with non-normative integration guidance + fixtures/journeys. Remaining gaps are mostly profile-quality and interoperability-hardening concerns, not blockers to execution.

Recommended posture:

- execute immediate integration work now,
- run targeted research tracks in parallel for high-risk security/privacy standardization,
- promote only evidence-backed profiles into broader conformance expectations.
