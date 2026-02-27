# Universal Manifest Threat Model

This document provides a comprehensive threat analysis for the Universal Manifest specification and reference implementations.

## Overview

Universal Manifest is a **portable state capsule** designed for local-first environments where consumers operate with partial connectivity and must validate state using cached, verifiable credentials. The threat model addresses security concerns across the entire lifecycle: issuance, distribution, verification, and revocation.

**Design Context:**

- **Local-first verification**: Manifests are verified on constrained devices (Android TV, edge boxes) without guaranteed network connectivity
- **Public distribution**: Manifests may be resolved via public HTTP endpoints (e.g., `myum-resolver`)
- **Cryptographic integrity**: v0.2 uses Ed25519 signatures with JCS (RFC 8785) canonicalization
- **Time-bounded validity**: All manifests include `issuedAt` and `expiresAt` timestamps

## Threat Categories

### 1. Replay Attacks

**Threat:**

An attacker intercepts a valid, signed manifest and re-presents it after its intended use window has passed, or presents it to a different consumer/context than intended.

**Attack Scenarios:**

- **Expired manifest replay**: Attacker captures a manifest and attempts to use it after `expiresAt`
- **Cross-context replay**: Attacker presents a manifest issued for one venue/device to a different venue
- **Stale state replay**: Attacker replays an old manifest that has been superseded by a newer version (e.g., after consent revocation)

**Mitigations:**

1. **TTL enforcement (REQUIRED)**: Verifiers MUST reject manifests where `now > expiresAt`. This is enforced in reference implementation at `/packages/universal-manifest/src/index.ts:238` (v0.1) and line 371 (v0.2).

2. **Short-lived manifests**: Issuers SHOULD use TTLs appropriate to the use case:
   - Venue check-in: 5-60 minutes
   - Device registration: 1-24 hours
   - Long-lived consent grants: consider including revocation metadata

3. **Nonce/jti (optional)**: For high-security contexts, issuers MAY include a unique `jti` (JWT ID) claim and consumers MAY maintain a short-lived nonce registry to prevent replay within the TTL window.

4. **Context binding (optional)**: For cross-context replay prevention, issuers MAY include audience claims (e.g., `aud` field) binding the manifest to a specific venue/device. Consumers SHOULD validate audience claims when present.

**Residual Risk:**

Within the TTL window, a manifest can be replayed unless nonce/jti or audience validation is implemented. This is acceptable for many use cases where TTLs are short (< 5 minutes).

### 2. Manifest Tampering

**Threat:**

An attacker modifies manifest contents in transit or at rest to alter permissions, identity claims, or expiration dates.

**Attack Scenarios:**

- **Permission escalation**: Attacker modifies `consents` array to grant elevated permissions
- **Identity substitution**: Attacker changes `subject` field to impersonate another user
- **TTL extension**: Attacker extends `expiresAt` to make manifest valid longer
- **Signature stripping**: Attacker removes `signature` field and presents unsigned manifest (see §7)

**Mitigations:**

1. **Cryptographic signature verification (v0.2, REQUIRED)**: The v0.2 signature profile uses Ed25519 signatures over JCS-canonicalized manifest contents (excluding the `signature` field). Any modification to signed fields invalidates the signature. Verification is enforced at `/packages/universal-manifest/src/index.ts:272-302` (signature verification function).

2. **Canonical signing input**: JCS (RFC 8785) eliminates ambiguity in JSON representation, ensuring the same logical manifest produces identical signing input across implementations.

3. **Signature field exclusion**: The `signature` field is removed before canonicalization (line 280), preventing circular dependencies and ensuring signature covers all other fields.

4. **Structural validation**: Reference implementation validates required fields, type constraints, and timestamp ordering (`issuedAt <= expiresAt`) before signature verification.

**v0.1 Limitation:**

v0.1 `signature` field is intentionally permissive and not interoperable. **v0.1 manifests MUST NOT be used in production security-critical contexts.** Implementations SHOULD migrate to v0.2 for tamper protection.

**Residual Risk:**

If a verifier incorrectly implements canonicalization or signature verification, tampering may go undetected. Implementers MUST use test vectors from `/spec/v0.2/CONFORMANCE.md` to validate correctness.

### 3. Key Compromise

**Threat:**

An attacker obtains the private signing key used by an issuer, enabling them to forge valid manifests.

**Attack Scenarios:**

- **Key theft**: Private key stolen from issuer infrastructure via breach, insider threat, or supply chain attack
- **Key leakage**: Private key accidentally committed to version control, logged, or exposed via misconfigured services
- **Cryptographic weakness**: Use of weak key generation or side-channel attacks against key material

**Mitigations:**

1. **Key rotation**: Issuers MUST rotate signing keys regularly (see §8, Key Rotation and Revocation).

2. **Hardware security modules (HSMs)**: For production issuers, private keys SHOULD be stored in HSMs or secure enclaves with access controls.

3. **Key generation**: Use cryptographically secure random number generators (CSPRNGs) for key generation. The reference implementation uses `node:crypto` which delegates to OS-level CSPRNGs.

4. **Revocation support**: v0.2 includes `signature.statusRef` and `signature.revocationCursor` fields to enable revocation-aware verification. When key compromise is detected, issuers MUST:
   - Mark all manifests signed with compromised key as revoked
   - Publish revocation status at `signature.statusRef` endpoints
   - Rotate to new keys immediately

5. **Short-lived keys (recommended)**: For high-volume issuers, use short-lived signing keys (e.g., 30-90 days) to limit blast radius of compromise.

**Residual Risk:**

If a key is compromised and the attacker forges manifests before revocation mechanisms are activated, those manifests will verify successfully until they expire (`expiresAt`). This is mitigated by short TTLs and rapid incident response.

### 4. Revocation Bypass

**Threat:**

An attacker presents a revoked manifest to a consumer that fails to check revocation status, or exploits stale revocation data.

**Attack Scenarios:**

- **Offline verification bypass**: Consumer verifies signature but skips revocation check due to network unavailability
- **Stale cache exploitation**: Consumer uses outdated revocation status from cache while attacker races to use revoked manifest
- **Status endpoint unavailability**: Attacker DoS attacks `signature.statusRef` endpoint to force consumers into offline mode

**Mitigations:**

1. **Revocation-aware verification (v0.2, optional)**: Consumers implementing revocation-aware verification MUST:
   - Fetch revocation status from `signature.statusRef` (when present)
   - Enforce `signature.revocationCursor` monotonicity to prevent stale-status acceptance
   - Reject manifests when revocation status is `revoked`
   - Report verification status as `unchecked` when revocation cannot be determined

   Reference: `/spec/v0.2/SIGNATURE-PROFILE.md:136-144`

2. **Policy-based enforcement**: Consumers SHOULD define revocation policies appropriate to their risk model:
   - **High-security contexts**: Require active revocation check; reject manifests when status unavailable
   - **Low-connectivity contexts**: Accept `unchecked` status but log for audit
   - **Short-lived manifests**: Rely on TTL expiration; revocation checks optional

3. **Cache revalidation**: Consumers MUST use `signature.revocationCursor` to detect stale cached status. When cursor changes, consumers MUST refetch status before accepting manifest.

4. **Short revocation propagation SLAs**: Issuers SHOULD publish revocation updates within minutes of revocation decision and design `statusRef` endpoints for high availability.

**Residual Risk:**

In fully offline scenarios (no network access to `statusRef`), revocation cannot be enforced. Consumers relying solely on signature verification accept this risk and MUST document their verification posture as "revocation-unchecked."

### 5. Denial of Service (DoS)

**Threat:**

An attacker submits oversized, deeply nested, or computationally expensive manifests to exhaust consumer resources (CPU, memory, network bandwidth).

**Attack Scenarios:**

- **Oversized manifests**: Multi-megabyte manifests containing large embedded data (e.g., base64-encoded images in shards)
- **Deep nesting**: Manifests with deeply nested `shards` or entity structures that exhaust stack/heap during parsing
- **Algorithmic complexity attacks**: Manifests with thousands of shards or claims, triggering O(n²) validation loops
- **Signature verification DoS**: Flooding verifier with invalid signatures to consume CPU resources

**Mitigations:**

1. **Size limits (REQUIRED)**:

   - **Resolver-enforced limits**: The `myum-resolver` reference implementation SHOULD enforce maximum manifest size. Recommended limit: **1 MB** for JSON payload.

   - **Consumer-enforced limits**: Consumers MUST validate manifest size before parsing. Recommended limits:
     - Total JSON size: 1 MB
     - Individual shard size: 100 KB
     - Array lengths: 1,000 elements max per array (`shards`, `claims`, etc.)

2. **Depth limits (REQUIRED)**:

   - **Maximum nesting depth**: Consumers MUST enforce a maximum JSON object depth. Recommended limit: **10 levels**.

   - **Shard composition limits**: Consumers SHOULD limit the number of shards per manifest (recommended: 100 shards max).

3. **Early rejection**:

   - Consumers SHOULD validate size/depth limits BEFORE signature verification to avoid wasting CPU on invalid manifests.

   - HTTP resolvers (e.g., `myum-resolver`) SHOULD return `413 Payload Too Large` for oversized manifests.

4. **Rate limiting**:

   - Resolver endpoints SHOULD implement rate limiting per IP/client (e.g., 100 requests/minute).

   - Reference implementation at `/services/myum-resolver/src/index.ts` uses Cloudflare Workers which provides built-in DDoS protection.

5. **Streaming parsing (optional)**: For very large manifests, consumers MAY use streaming JSON parsers that enforce limits incrementally.

**Recommended Limits Summary:**

| Resource | Limit | Enforcement Point |
|----------|-------|-------------------|
| Total manifest size | 1 MB | Resolver + Consumer |
| Individual shard size | 100 KB | Consumer |
| JSON nesting depth | 10 levels | Consumer (parser config) |
| Shards per manifest | 100 | Consumer |
| Array element counts | 1,000 | Consumer |
| Signature verification attempts | Rate-limited | Resolver |

**Residual Risk:**

Consumers that fail to enforce these limits may be vulnerable to resource exhaustion. Implementers MUST test against adversarial inputs (see conformance suite).

### 6. Privacy Leakage

**Threat:**

Manifest contents or resolution patterns leak sensitive information about users, their activities, or their relationships.

**Attack Scenarios:**

- **PII exposure**: Manifests include personally identifiable information (names, emails, biometrics) in plaintext
- **Correlation attacks**: Attacker correlates manifest `@id` or `subject` values across multiple resolvers to track user movements
- **Resolver logging**: Public resolvers log manifest IDs and client IPs, enabling surveillance
- **Cache poisoning**: Attacker injects manifests into shared caches to track which consumers request them

**Mitigations:**

1. **Opaque identifiers**:

   - Manifest `@id` SHOULD use `urn:uuid:<uuidv4>` (random, globally unique, non-correlatable).

   - Issuers MUST rotate `@id` per issuance to prevent cross-context correlation.

   - Reference: `/spec/v0.1/README.md:51`

2. **Subject privacy**:

   - `subject` field typically contains a DID or pseudonymous identifier. Issuers SHOULD use **pairwise DIDs** (unique per relationship) to prevent correlation across contexts.

   - Avoid including direct PII in `subject` (use indirect references or encrypted payloads).

3. **Minimal disclosure**:

   - Manifests SHOULD include only claims/consents necessary for the immediate use case.

   - Use selective disclosure techniques (e.g., zero-knowledge proofs or BBS+ signatures) for advanced privacy (future extension).

4. **Resolver privacy posture**:

   - Public resolvers (e.g., `myum-resolver`) assume manifests are **publicly readable** (see line 175-176 in `/services/myum-resolver/src/index.ts`).

   - For private manifests, use authenticated resolution endpoints (out of scope for v0.1/v0.2).

   - Resolver logs SHOULD retain only minimal telemetry (manifest `@id` hash, not full contents).

5. **Transport encryption**:

   - Resolver endpoints MUST use HTTPS to prevent eavesdropping on manifest contents in transit.

   - Reference implementation enforces HTTPS (Cloudflare Workers automatically upgrades HTTP).

6. **Cache control**:

   - Resolvers SHOULD use short cache TTLs (`Cache-Control: public, max-age=60`) to limit stale-data exposure.

   - Consumers MUST NOT cache manifests beyond their `expiresAt` timestamp.

**Privacy Model Summary:**

- **v0.1/v0.2 baseline**: Manifests are assumed to be **semi-public** (accessible to anyone who knows the manifest `@id`).
- **Private use cases**: Require authentication layers above the Universal Manifest protocol (e.g., OAuth2-protected resolvers).

**Residual Risk:**

Universal Manifest does not currently support end-to-end encryption or zero-knowledge selective disclosure. Use cases requiring strong privacy SHOULD layer encryption above the base protocol (e.g., JWE envelopes).

### 7. Signature Stripping

**Threat:**

An attacker removes the `signature` field from a v0.2 manifest and presents it to a verifier that fails to enforce signature requirements, or downgrades to v0.1 permissive mode.

**Attack Scenarios:**

- **Downgrade to v0.1**: Attacker modifies `manifestVersion` from `"0.2"` to `"0.1"` and removes `signature`, bypassing v0.2 verification
- **Permissive verifier**: Verifier treats `signature` as optional and accepts unsigned manifests
- **Partial verification**: Verifier checks signature if present but accepts absence without error

**Mitigations:**

1. **Mandatory signature (v0.2)**:

   - The v0.2 schema requires `signature` field (see `/packages/universal-manifest/src/index.ts:106-121`).

   - Verifiers MUST reject v0.2 manifests missing `signature` field before any other processing.

2. **Strict version enforcement**:

   - Verifiers MUST validate `manifestVersion` matches expected version before applying version-specific validation rules.

   - Consumers SHOULD maintain a **policy allowlist** of accepted `manifestVersion` values (e.g., only accept `"0.2"` in production).

3. **Profile identification (v0.2)**:

   - Verifiers MUST check `signature.algorithm === "Ed25519"` and `signature.canonicalization === "JCS-RFC8785"`.

   - Unknown or unsupported profiles MUST be rejected when strict verification is required.

   - Reference: `/spec/v0.2/SIGNATURE-PROFILE.md:129-134`

4. **Fail-closed verification**:

   - Verifiers MUST default to **reject** when signature verification fails or signature is absent.

   - Explicitly document verification posture (e.g., "strict v0.2 signature required" vs. "v0.1 permissive mode").

**Residual Risk:**

If a verifier incorrectly implements version/profile checks, an attacker may succeed in presenting unsigned manifests. Implementers MUST test against negative test vectors (unsigned manifests, wrong versions, invalid signatures).

## 8. Key Rotation and Revocation Operational Guidance

This section provides operational best practices for issuers managing signing keys and revocation infrastructure.

### Key Rotation Strategy

**Recommended rotation frequency:**

- **Short-lived keys (high-volume issuers)**: Rotate every 30-90 days
- **Long-lived keys (low-volume issuers)**: Rotate every 6-12 months
- **Emergency rotation**: Immediately upon suspected compromise

**Rotation procedure:**

1. **Generate new key pair**: Use cryptographically secure key generation (Ed25519, 256-bit seed).

2. **Publish new public key**:
   - Update key material at `signature.keyRef` endpoints (DID documents or HTTPS URLs)
   - Maintain old keys accessible for verification of unexpired manifests

3. **Transition period**: For 24-48 hours, sign new manifests with new key while old manifests remain valid.

4. **Deprecate old key**: After transition, mark old key as `revoked` in key metadata and stop using for new signatures.

5. **Overlap validation window**: Ensure old key remains available for verification until all manifests signed with it have expired (`expiresAt` passed).

### Revocation Infrastructure

**Required components for revocation-aware verification:**

1. **Status endpoint (`signature.statusRef`)**:
   - HTTPS endpoint returning revocation status for manifest or key
   - Format: JSON with `{"status": "active" | "revoked", "cursor": "<monotonic-version>"}`
   - SLA: 99.9% uptime, < 100ms response time

2. **Revocation cursor (`signature.revocationCursor`)**:
   - Monotonically increasing version identifier (e.g., Unix timestamp, version counter)
   - Consumers use cursor to detect stale cached status
   - Update cursor whenever revocation status changes

3. **Revocation propagation**:
   - Publish revocation updates within 5 minutes of revocation decision
   - Use CDN edge caching with short TTLs (60 seconds) for global distribution

**Revocation events:**

- **Key compromise**: Revoke all manifests signed with compromised key
- **Subject request**: User requests revocation of their manifest (e.g., consent withdrawal)
- **Policy violation**: Manifest found to violate issuer policies post-issuance

**Monitoring and logging:**

- Log all revocation events with timestamps and reasons
- Monitor `statusRef` endpoint availability and latency
- Alert on unusual revocation patterns (potential compromise indicator)

### Emergency Response

**If key compromise is detected:**

1. **Immediate actions** (< 1 hour):
   - Revoke compromised key in key metadata
   - Update all `statusRef` endpoints to mark affected manifests as revoked
   - Rotate to new key pair
   - Notify relying parties via security contact

2. **Short-term** (< 24 hours):
   - Audit all manifests signed with compromised key
   - Issue new manifests to affected subjects with new signatures
   - Publish incident report at security contact endpoint

3. **Long-term** (< 7 days):
   - Conduct forensic analysis of compromise root cause
   - Implement additional key protection measures (HSM, access controls)
   - Update key rotation frequency if needed

## 9. Size and Depth Limits Reference

### Recommended Consumer Limits

```typescript
// Example validation configuration
const MANIFEST_LIMITS = {
  maxTotalBytes: 1_048_576,        // 1 MB total JSON
  maxShardBytes: 102_400,           // 100 KB per shard
  maxNestingDepth: 10,              // JSON object depth
  maxShards: 100,                   // Shards per manifest
  maxArrayElements: 1_000,          // Claims, consents, devices, etc.
  maxStringLength: 10_000,          // Individual string fields
}
```

### Implementation Example

```typescript
function validateManifestSize(manifest: unknown): void {
  const json = JSON.stringify(manifest)
  if (json.length > MANIFEST_LIMITS.maxTotalBytes) {
    throw new Error(`Manifest exceeds size limit: ${json.length} bytes`)
  }

  // Validate nesting depth (requires custom parser or recursive check)
  const depth = computeJsonDepth(manifest)
  if (depth > MANIFEST_LIMITS.maxNestingDepth) {
    throw new Error(`Manifest exceeds nesting depth: ${depth}`)
  }

  // Validate array sizes
  if (Array.isArray((manifest as any).shards)) {
    if ((manifest as any).shards.length > MANIFEST_LIMITS.maxShards) {
      throw new Error(`Too many shards: ${(manifest as any).shards.length}`)
    }
  }
}
```

Consumers MUST call `validateManifestSize()` before signature verification or semantic processing.

## 10. Defense in Depth

The Universal Manifest security model relies on **layered defenses**:

1. **Cryptographic integrity** (v0.2 signatures) prevents tampering
2. **Time-bounded validity** (TTL enforcement) limits replay window
3. **Revocation infrastructure** enables post-issuance invalidation
4. **Resource limits** (size/depth) prevent DoS
5. **Privacy-conscious design** (opaque IDs, minimal disclosure) reduces leakage
6. **Fail-closed verification** (strict profile checks) prevents downgrade attacks

**No single mitigation is sufficient.** Implementers MUST adopt all applicable mitigations for their threat model.

## 11. Threat Assessment Summary

| Threat | Severity | v0.2 Mitigation | Residual Risk |
|--------|----------|-----------------|---------------|
| Replay attacks | Medium | TTL enforcement (required) | Within-TTL replay (low) |
| Manifest tampering | Critical | Ed25519 signatures (required) | Implementation bugs (low) |
| Key compromise | High | Key rotation + revocation (recommended) | Pre-revocation forgery (medium) |
| Revocation bypass | Medium | Revocation-aware verification (optional) | Offline scenarios (medium) |
| DoS (oversized manifests) | Medium | Size/depth limits (required) | Non-compliant consumers (medium) |
| Privacy leakage | Medium | Opaque IDs, minimal disclosure (required) | Correlation across contexts (low) |
| Signature stripping | High | Mandatory signature (v0.2 required) | Version downgrade (low) |

**Severity levels:**

- **Critical**: Enables arbitrary manifest forgery or complete protocol bypass
- **High**: Enables targeted attacks with significant impact
- **Medium**: Requires specific conditions or affects limited scenarios
- **Low**: Minimal impact or requires substantial attacker resources

## 12. Conformance and Testing

Implementers MUST validate their security implementation against test vectors in:

- `/spec/v0.2/CONFORMANCE.md` (structural validation, signature verification)
- Adversarial test fixtures (oversized manifests, invalid signatures, tampered fields)

**Required negative tests:**

1. Expired manifest (past `expiresAt`)
2. Unsigned v0.2 manifest
3. Tampered signature value
4. Modified signed fields (changed `subject`, extended `expiresAt`)
5. Oversized manifest (> 1 MB)
6. Deeply nested JSON (> 10 levels)
7. Unknown signature algorithm
8. Missing required fields

## 13. Security Contact

Report security vulnerabilities to: **security@universalmanifest.net**

Do NOT open public GitHub issues for security issues.

See `/SECURITY.md` for reporting guidelines and response timelines.

## 14. References

- **v0.2 Signature Profile**: `/spec/v0.2/SIGNATURE-PROFILE.md`
- **v0.1 Spec**: `/spec/v0.1/README.md`
- **v0.2 Spec**: `/spec/v0.2/README.md`
- **Reference Verifier**: `/packages/universal-manifest/src/index.ts`
- **Reference Resolver**: `/services/myum-resolver/src/index.ts`
- **RFC 8785 (JCS)**: https://www.rfc-editor.org/rfc/rfc8785.html
- **Ed25519**: https://ed25519.cr.yp.to/
