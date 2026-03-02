# Universal Manifest Migration Guide: v0.1 to v0.2

**Status:** Active draft
**Updated:** 2026-03-02
**Audience:** Implementers maintaining v0.1 consumers/issuers
**Normative references:** `spec/v0.1/`, `spec/v0.2/`, `spec/v0.2/SIGNATURE_PROFILE.md`

## 1. Understand What Changed

Universal Manifest v0.2 keeps the v0.1 core document shape and forward-compatibility rules, but adds a deterministic signature profile for interoperable trust checks.

### 1.1 Change classification

| Change | Classification | Impact if unchanged |
|---|---|---|
| `manifestVersion` value moves from `"0.1"` to `"0.2"` | breaking-consumer + breaking-issuer | Strict version checks fail for unknown/new version values |
| `signature` moves from permissive placeholder to required profile for v0.2 conformance | breaking-consumer + breaking-issuer | v0.2 consumers reject unsigned manifests; v0.1 issuers cannot satisfy v0.2 consumers |
| Consumers in v0.2 verify JCS + Ed25519 signatures | breaking-consumer | Tampered payloads may be accepted if verification is not implemented |
| Required core fields remain unchanged (`@context`, `@id`, `@type`, `manifestVersion`, `subject`, `issuedAt`, `expiresAt`) | unchanged | Existing field parsing logic remains reusable |
| Unknown-field tolerance remains required | unchanged | Forward-compatibility behavior should remain stable |
| TTL enforcement remains required (`issuedAt <= expiresAt`, reject if expired for use) | unchanged | Existing time-window logic remains reusable |
| `signature.algorithm`, `signature.canonicalization`, `signature.publicKeySpkiB64` or `signature.keyRef`, `signature.created`, `signature.value` become operationally relevant for conformance | additive + breaking when migrating to strict v0.2 support | Missing values prevent v0.2 verification |
| `signature.statusRef` and `signature.revocationCursor` can be carried for revocation-aware workflows | additive | Baseline verifiers can ignore these fields unless implementing extended profile |

## 2. Compatibility Matrix

| Scenario | Behavior | Action required |
|---|---|---|
| v0.1 consumer receives v0.2 manifest | Consumer ignores unknown signature subfields and can still parse payload structurally (graceful degradation), but does not provide v0.2 trust guarantees | Upgrade consumer to v0.2 verification for tamper protection |
| v0.2 consumer receives v0.1 manifest | Consumer cannot satisfy v0.2 signature verification requirements for a v0.2-only flow | Add dual-version support or require issuer upgrade |
| v0.1 issuer sends to v0.2-only consumer | Rejected in strict v0.2-only policy because signature profile is missing | Upgrade issuer to produce signed v0.2 manifests |
| v0.2 issuer sends to v0.1 consumer | Typically accepted by v0.1 parser due to unknown-field tolerance | No immediate action; plan consumer upgrade for trust checks |
| Mixed environment | Outcome depends on explicit acceptance policy per surface | Document and enforce a rollout policy with sunset date |

### 2.1 Recommended dual-version strategy

1. Parse manifest JSON as usual.
2. Switch logic by `manifestVersion`.
3. For `"0.1"`: enforce v0.1 structure + TTL.
4. For `"0.2"`: enforce v0.2 structure + signature verification.
5. Reject unknown versions unless explicitly allowed in a staged rollout.
6. Emit telemetry indicating version so you can measure v0.1 retirement readiness.

## 3. Migrate Your Consumer

### Step 1: Add version-aware validation

- Keep your current v0.1 validation path.
- Add a separate v0.2 validation path keyed by `manifestVersion`.

### Step 2: Add JCS canonicalization

- Use an RFC 8785-compliant canonicalizer.
- Canonicalize the manifest with `signature` removed before verification.

### Step 3: Add Ed25519 verification

- Accept either `signature.publicKeySpkiB64` (embedded key material) or `signature.keyRef` (externally resolved key).
- Verify `signature.value` over canonicalized bytes.

### Step 4: Enforce v0.2 signature profile checks

- `signature.algorithm` must be `"Ed25519"`.
- `signature.canonicalization` must be `"JCS-RFC8785"`.
- `signature.created` must be parseable ISO date-time.

### Step 5: Update failure behavior

- If signature verification fails, reject for use.
- Keep diagnostic reasons structured and machine-readable where possible.

### TypeScript example (consumer path)

```ts
import {
  assertUniversalManifestV01,
  assertUniversalManifestV02,
  verifyUniversalManifestV02,
  type UniversalManifestV01,
  type UniversalManifestV02,
} from "universal-manifest";

export function validateForUse(manifest: unknown, now = new Date()):
  | { version: "0.1"; manifest: UniversalManifestV01 }
  | { version: "0.2"; manifest: UniversalManifestV02 } {
  const obj = manifest as Record<string, unknown>;
  const version = obj?.manifestVersion;

  if (version === "0.1") {
    const v01 = assertUniversalManifestV01(manifest, { now });
    return { version: "0.1", manifest: v01 };
  }

  if (version === "0.2") {
    const v02 = assertUniversalManifestV02(manifest, { now });
    const verification = verifyUniversalManifestV02(v02, { now });
    if (!verification.ok) {
      throw new Error(`v0.2 verification failed: ${verification.reason ?? "unknown"}`);
    }
    return { version: "0.2", manifest: v02 };
  }

  throw new Error(`Unsupported manifestVersion: ${String(version)}`);
}
```

## 4. Migrate Your Issuer

### Step 1: Provision signing keys

- Generate Ed25519 keypair.
- Store private key in your issuer trust boundary.
- Publish public key by `keyRef` URL (or embed SPKI for constrained deployments).

### Step 2: Add canonicalization + signing

- Create unsigned manifest payload.
- Canonicalize payload (without `signature`).
- Sign canonical bytes with Ed25519.

### Step 3: Emit v0.2 signature block

- Include algorithm, canonicalization, created timestamp, and key material reference.

### Step 4: Keep TTL and unknown-field behavior unchanged

- Migration to v0.2 does not replace TTL and forward-compatibility obligations.

### TypeScript example (issuer path)

```ts
import {
  createUnsignedManifestV02,
  signUniversalManifestV02,
} from "universal-manifest";

export async function issueSignedManifest(input: {
  subject: string;
  ttlSeconds: number;
  privateKeyPkcs8Pem: string;
  keyRef: string;
}) {
  const unsigned = createUnsignedManifestV02({
    subject: input.subject,
    ttlSeconds: input.ttlSeconds,
    shards: [],
  });

  return signUniversalManifestV02(unsigned, {
    privateKeyPkcs8Pem: input.privateKeyPkcs8Pem,
    keyRef: input.keyRef,
    created: new Date().toISOString(),
  });
}
```

## 5. Mixed-Environment Rollout Plan

1. Start with dual-version consumer support.
2. Upgrade issuers to produce v0.2 in internal/staging lanes.
3. Publish v0.2 acceptance policy and migration date.
4. Run both v0.1 and v0.2 conformance tracks during overlap.
5. Freeze new feature work on v0.1.
6. Enforce v0.2-only once adopter telemetry shows readiness.

## 6. Verify Your Migration

### 6.1 Conformance verification

- Run v0.1 and v0.2 fixtures during overlap.
- Use the standalone conformance runner from `conformance/runner`.
- Store generated conformance report JSON as release evidence.

### 6.2 Backward-compatibility verification

- Confirm v0.1 acceptance path still works for explicitly-allowed legacy inputs.
- Confirm v0.2 signatures fail closed (tampered manifests rejected).

### 6.3 Operational checks

- Resolver behavior unchanged for UMID lookup surfaces.
- Deploy smoke checks pass before production promotion.

## 7. Key Generation and Rotation Guidance

### 7.1 Generate Ed25519 keys (example)

```bash
openssl genpkey -algorithm Ed25519 -out issuer-ed25519-private.pem
openssl pkey -in issuer-ed25519-private.pem -pubout -out issuer-ed25519-public.pem
```

### 7.2 Key publication model

- Publish public key at a stable HTTPS URL (`signature.keyRef`).
- Keep key history accessible for manifests signed before rotation.

### 7.3 Rotation policy (recommended)

- Rotate signing keys on schedule (for example, every 90 days) or immediately on suspected compromise.
- Keep previous public keys available for a grace period aligned with manifest TTL and audit requirements.

## 8. Deprecation Timeline

v0.1 lifecycle policy is defined in `docs/governance/DEPRECATION-POLICY.md`.

Current project policy baseline:

- v0.1 remains supported for at least 6 months after v0.2 is declared stable.
- During overlap, both tracks remain in conformance suite evidence.
- After end-of-life, v0.1 fixtures remain available as legacy evidence but do not receive new features.

## 9. Frequently Asked Migration Questions

### Q: Do I need JSON-LD RDF processing to migrate to v0.2?
No. The v0.2 baseline profile is JSON canonicalization (JCS) plus Ed25519 signatures.

### Q: Can I use another signature algorithm and still claim v0.2 baseline conformance?
No. v0.2 baseline requires Ed25519 + JCS-RFC8785.

### Q: What if resolver lookup fails during migration?
Use your cached manifest only within valid TTL; fail closed for expired data.

### Q: Is TypeScript required for migration?
No. TypeScript examples here are reference examples only. Any language can implement conformance behavior.

## 10. Related Documents

- `docs/guides/IMPLEMENTATION-GUIDE.md`
- `docs/guides/QUICK-REFERENCE.md`
- `docs/governance/DEPRECATION-POLICY.md`
- `docs/governance/BREAKING-CHANGE-POLICY.md`
- `spec/v0.2/SIGNATURE_PROFILE.md`
