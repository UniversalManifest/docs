---
work_order: WO-0055
agent_task_id: e0a7fe60_1772165606
spec_versions_covered:
  - "0.1"
  - "0.2"
updated: "2026-03-02"
conformance_suite_version: "0.1.0"
---

# Universal Manifest Implementation Guide

Universal Manifest (UM) is an open specification. It is not bound to one language or runtime. The TypeScript helper and the standalone `um-typescript` repository are reference implementations, not normative requirements.

This guide is a full implementation path from first parse to conformance report submission.

## 1. Introduction

### What is Universal Manifest

Universal Manifest is a portable JSON-LD envelope for identity/state exchange. A conformant implementation parses required fields, enforces TTL, safely ignores unknown fields, and (for v0.2) verifies signatures with the published profile.

### What this guide covers

- How to choose a conformance target.
- How to build consumer and issuer behavior.
- How to add v0.2 signing and verification.
- How to run the conformance suite and publish results.

### Prerequisites

- Ability to parse JSON and RFC 3339 timestamps.
- Access to your language's Ed25519 and JCS (RFC 8785) libraries for v0.2.
- Access to the UM spec and conformance fixture artifacts.

### Normative vs informative markers

- `NORMATIVE REFERENCE`: behavior defined by versioned spec/conformance docs.
- `INFORMATIVE GUIDANCE`: implementation strategy and examples.

## 2. Choose Your Conformance Level

![Conformance decision tree](../../site/public/diagrams/conformance-decision-tree.svg)

Diagram source: `docs/diagrams/conformance-decision-tree.excalidraw`

Text fallback (non-visual):

1. If you only consume manifests, start with `v0.1-baseline` consumer.
2. If you produce manifests, implement `v0.1-baseline` issuer requirements as well.
3. If you need tamper protection, add `v0.2-baseline` signature verification/signing.
4. If you need revocation-aware verification, target `v0.2-extended`.

Conformance levels:

- `v0.1-baseline`: required fields, TTL, unknown-field tolerance.
- `v0.2-baseline`: v0.1 baseline plus JCS + Ed25519 signature profile.
- `v0.2-extended`: v0.2 baseline plus revocation-aware verification policy.

## 3. Step 1: Parse and Validate a Manifest

### NORMATIVE REFERENCE

Source of truth:

- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.2/CONFORMANCE.md`

Minimum required fields (`v0.1` and `v0.2`):

- `@context`
- `@id`
- `@type` (must include `um:Manifest`)
- `manifestVersion`
- `subject`
- `issuedAt`
- `expiresAt`

Required behavior:

- Parse JSON object.
- Reject missing/empty required fields.
- Parse `issuedAt` and `expiresAt` as RFC 3339 timestamps.
- Reject for use when `now > expiresAt`.
- Safely ignore unknown fields.

### INFORMATIVE GUIDANCE

Recommended validation order:

1. Shape check (object + required fields).
2. `@type` check (`um:Manifest` present in string or array form).
3. Timestamp parsing + `issuedAt <= expiresAt`.
4. TTL check (`now <= expiresAt`).

TypeScript (reference-style):

```ts
export function validateForUse(manifest: Record<string, unknown>, now = new Date()): void {
  const required = ['@context', '@id', '@type', 'manifestVersion', 'subject', 'issuedAt', 'expiresAt']
  for (const key of required) {
    if (!(key in manifest)) throw new Error(`missing required field: ${key}`)
  }

  const t = manifest['@type']
  const hasManifestType = typeof t === 'string'
    ? t === 'um:Manifest'
    : Array.isArray(t) && t.includes('um:Manifest')
  if (!hasManifestType) throw new Error('invalid @type')

  const issued = new Date(String(manifest['issuedAt']))
  const expires = new Date(String(manifest['expiresAt']))
  if (Number.isNaN(issued.getTime()) || Number.isNaN(expires.getTime())) throw new Error('invalid timestamp')
  if (issued > expires) throw new Error('issuedAt must be <= expiresAt')
  if (now > expires) throw new Error('manifest expired')
}
```

Python pseudocode:

```python
required = ["@context", "@id", "@type", "manifestVersion", "subject", "issuedAt", "expiresAt"]
for k in required:
    if k not in manifest:
        raise ValueError(f"missing {k}")

manifest_type = manifest["@type"]
if isinstance(manifest_type, str):
    ok = manifest_type == "um:Manifest"
else:
    ok = "um:Manifest" in manifest_type
if not ok:
    raise ValueError("invalid @type")

issued = parse_rfc3339(manifest["issuedAt"])
expires = parse_rfc3339(manifest["expiresAt"])
if issued > expires or now() > expires:
    raise ValueError("invalid validity window")
```

Go pseudocode:

```go
func ValidateForUse(m map[string]any, now time.Time) error {
    required := []string{"@context", "@id", "@type", "manifestVersion", "subject", "issuedAt", "expiresAt"}
    for _, k := range required {
        if _, ok := m[k]; !ok {
            return fmt.Errorf("missing %s", k)
        }
    }
    // Ignore unknown fields by default: only read keys your implementation supports.
    return nil
}
```

## 4. Step 2: Create a Manifest (Issuer)

### NORMATIVE REFERENCE

Issuer responsibilities are defined in:

- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.2/CONFORMANCE.md`

Required issuer decisions:

- `@id`: globally unique URI (recommended `urn:uuid:<uuidv4>`).
- `subject`: stable subject URI.
- TTL (`issuedAt`, `expiresAt`): explicit validity window.
- `manifestVersion`: exact version string (`"0.1"` or `"0.2"`).

### INFORMATIVE GUIDANCE

- Keep TTL short for active surfaces.
- Use opaque IDs to reduce cross-context correlation.
- Keep payload minimal; use pointers for large/off-chain data.

Example issuer payload (`v0.1`):

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld",
  "@id": "urn:uuid:af58f76e-a8f8-4b3a-bf2f-c8b8bb76a8de",
  "@type": "um:Manifest",
  "manifestVersion": "0.1",
  "subject": "did:key:z6Mki...",
  "issuedAt": "2026-03-02T00:00:00Z",
  "expiresAt": "2026-03-02T12:00:00Z",
  "facets": []
}
```

## 5. Step 3: Sign a Manifest (v0.2)

### NORMATIVE REFERENCE

v0.2 signature profile:

- `spec/v0.2/SIGNATURE-PROFILE.md`
- `spec/v0.2/CONFORMANCE.md`

Required profile values:

- `signature.algorithm`: `Ed25519`
- `signature.canonicalization`: `JCS-RFC8785`

Signing input rule:

1. Remove `signature` from the object.
2. Canonicalize remaining JSON with JCS (RFC 8785).
3. Sign canonical bytes with Ed25519.

### INFORMATIVE GUIDANCE

TypeScript (reference-style):

```ts
import canonicalize from 'canonicalize'
import { sign } from '@noble/ed25519'

export async function signManifestV02(manifest: Record<string, unknown>, privateKey: Uint8Array) {
  const unsigned = { ...manifest }
  delete unsigned.signature
  const canonical = canonicalize(unsigned)
  if (!canonical) throw new Error('failed to canonicalize manifest')

  const bytes = new TextEncoder().encode(canonical)
  const sig = await sign(bytes, privateKey)

  return {
    ...unsigned,
    signature: {
      algorithm: 'Ed25519',
      canonicalization: 'JCS-RFC8785',
      created: new Date().toISOString(),
      value: toBase64Url(sig)
    }
  }
}
```

Python pseudocode:

```python
unsigned = dict(manifest)
unsigned.pop("signature", None)
canonical_bytes = jcs_canonicalize(unsigned)
signature = ed25519_sign(private_key, canonical_bytes)
manifest["signature"] = {
    "algorithm": "Ed25519",
    "canonicalization": "JCS-RFC8785",
    "created": now_iso8601(),
    "value": base64url(signature),
}
```

## 6. Step 4: Verify a Manifest (v0.2)

### NORMATIVE REFERENCE

Required verification flow is defined in:

- `spec/v0.2/CONFORMANCE.md`
- `spec/v0.2/SIGNATURE-PROFILE.md`

Verification algorithm:

1. Run baseline checks (required fields + TTL + unknown-field tolerance behavior).
2. Validate profile pair (`Ed25519`, `JCS-RFC8785`).
3. Obtain public key (`signature.publicKeySpkiB64` or resolved `signature.keyRef`).
4. Recompute canonical signing bytes (`manifest` without `signature`).
5. Verify Ed25519 signature; reject if invalid.

### INFORMATIVE GUIDANCE

Error categories to expose in your API/reporting:

- `structural_error`
- `expired_manifest`
- `unsupported_profile`
- `key_resolution_error`
- `signature_invalid`

TypeScript verification sketch:

```ts
import canonicalize from 'canonicalize'
import { verify } from '@noble/ed25519'

export async function verifyManifestV02(manifest: Record<string, unknown>, publicKey: Uint8Array): Promise<boolean> {
  const sig = manifest.signature as { value?: string; algorithm?: string; canonicalization?: string }
  if (!sig || sig.algorithm !== 'Ed25519' || sig.canonicalization !== 'JCS-RFC8785' || !sig.value) {
    return false
  }

  const unsigned = { ...manifest }
  delete unsigned.signature
  const canonical = canonicalize(unsigned)
  if (!canonical) return false

  const msg = new TextEncoder().encode(canonical)
  return verify(fromBase64Url(sig.value), msg, publicKey)
}
```

Go pseudocode:

```go
if sig.Algorithm != "Ed25519" || sig.Canonicalization != "JCS-RFC8785" {
    return ErrUnsupportedProfile
}
unsigned := cloneWithoutSignature(manifest)
canon := JCS(unsigned)
if !ed25519.Verify(pubKey, canon, sigBytes) {
    return ErrInvalidSignature
}
```

## 7. Step 5: Run the Conformance Suite

### NORMATIVE REFERENCE

Conformance requirements are versioned in:

- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.2/CONFORMANCE.md`

### INFORMATIVE GUIDANCE

How to get the suite:

```bash
git clone https://github.com/grigb/universal-manifest.git
cd universal-manifest/conformance/runner
npm ci
```

Adapter contract (required by runner):

```json
{
  "result": "accept",
  "reason": "validated"
}
```

Run command-mode conformance:

```bash
node ./cli.mjs \
  --mode command \
  --adapter-command "python3 /path/to/adapter.py" \
  --conformance-root conformance \
  --versions 0.1,0.2 \
  --report ./conformance-report.json
```

Validate your report format against schema:

- schema: `conformance/schema/conformance-report.schema.json`
- suite version in current repository: `0.1.0`

## 8. Common Pitfalls and FAQ

Common pitfalls:

- Enforcing strict field allowlists (breaks forward compatibility).
- Verifying signatures before checking TTL and basic structure.
- Signing JSON without JCS canonicalization.
- Treating unsupported signature profiles as baseline-compatible.

FAQ:

1. What JSON-LD processing do I need?
- None for baseline conformance. Standard JSON parsing is sufficient.

2. Can I use a different signature algorithm for v0.2 conformance?
- No. v0.2 baseline conformance requires `Ed25519` + `JCS-RFC8785`.

3. How do I handle manifests with unknown fields?
- Ignore them safely. Do not reject solely because fields are unknown.

4. What is the minimum manifest size I should support?
- Support at least up to 1 MB per manifest.

5. How do I test my implementation?
- Run the conformance suite fixtures and compare results to `expected.json`.

6. Can I extend the manifest with custom fields?
- Yes. Extensions are allowed; unknown fields are forward-compatible.

7. What about privacy and GDPR concerns?
- Use opaque IDs, minimize disclosure, and prefer short TTLs for sensitive data.

8. How do I resolve a UMID?
- Perform HTTP GET to `https://myum.net/{UMID}`.

9. What if the resolver is down?
- Use cached manifests only within TTL. Expired manifests must not be used for authorization/render decisions.

## 9. Submitting Your Conformance Report

Prepare a final report package:

1. `conformance-report.json` produced by your runner.
2. Adapter/source revision identifier.
3. Runtime and implementation metadata (`name`, `version`, `language`, optional `organization`, optional `repository`).
4. Optional CI logs/artifacts proving repeatability.

Recommended submission path:

- Publish your report artifact in your implementation repository.
- Share the report URL and implementation repo URL with UM maintainers for interoperability tracking.

## Related resources

- Site guide: `https://universalmanifest.net/guides/implementation-guide/`
- Quick reference card: `https://universalmanifest.net/guides/quick-reference/`
- Portable Identity Profile XR path: `docs/guides/PORTABLE-IDENTITY-PROFILE-XR-IMPLEMENTATION-PATH.md`
- MUM synchronization profile: `docs/guides/MUM-SYNCHRONIZATION-PROFILE.md`
- Migration guide: `https://universalmanifest.net/guides/migration-v01-v02/`
- Agent handoff companion: `docs/guides/AGENT-HANDOFF.md`
- Reference implementation (TypeScript): `https://github.com/grigb/um-typescript`
