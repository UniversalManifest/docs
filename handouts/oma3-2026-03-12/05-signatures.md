# 05 -- Signatures and Integrity: Tamper Detection

---

## The Analogy

A wax seal on a letter serves two purposes: it proves who sent the letter (only the sender has the seal), and it proves the letter was not opened in transit (a broken seal means tampering). You check the seal before reading the letter. If the seal is broken, you do not trust the contents.

Universal Manifest v0.2 adds a digital equivalent. The issuer stamps the manifest with a cryptographic signature. Any consumer can verify the signature to confirm that the manifest was not modified in transit and that it was issued by the claimed source.

---

## Why

A portable document that travels between systems needs tamper detection. Without it, any intermediary could modify the manifest -- changing consent rules, altering identity fields, or injecting false claims. The receiving system would have no way to detect the change.

## What

The v0.2 specification adds a **signature profile** using two established standards:

- **Ed25519** for the signature algorithm -- fast, compact (64-byte signatures), widely implemented, no curve parameter negotiation needed.
- **JCS (JSON Canonicalization Scheme, RFC 8785)** for deterministic serialization -- ensures every implementation produces identical bytes from the same JSON, so the signature verifies consistently across platforms.

Signatures are modular. A consuming system verifies the profiles it supports and safely ignores unknown ones. Unknown fields in a signed manifest are preserved, not rejected. This ensures forward compatibility.

## How -- The Signature Block

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

### What each signature field means

| Field | Purpose |
|-------|---------|
| `algorithm` | The signing algorithm. Must be `"Ed25519"` in v0.2. |
| `canonicalization` | The serialization method. Must be `"JCS-RFC8785"`. This ensures identical bytes across implementations. |
| `keyRef` | Where to find the public key for verification. Typically a DID verification method URL. |
| `publicKeySpkiB64` | The public key itself, base64-encoded. This enables offline verification -- the consumer does not need to fetch the key separately. |
| `created` | When the signature was produced. |
| `value` | The actual signature bytes (base64url-encoded). |

### The signing process

1. Start with the complete manifest JSON
2. Remove the `signature` property entirely
3. Canonicalize the remaining JSON using JCS (RFC 8785) -- keys sorted lexicographically, no whitespace, deterministic number format
4. Sign the canonical bytes with Ed25519
5. Attach the signature block back to the manifest

### The verification process

A consumer verifies in reverse:

1. Remove the `signature` property from the manifest
2. Canonicalize the remaining JSON using JCS
3. Verify the Ed25519 signature against the canonical bytes using the public key

If verification fails, the manifest was modified. Reject it.

### What the signature covers

Everything in the manifest is signed except the signature block itself: `@context`, `@id`, `@type`, `subject`, `issuedAt`, `expiresAt`, all facets, all claims, all consents, all pointers. Changing any byte in any of these fields invalidates the signature.

---

*Next: [06 -- The Resolver](06-resolver.md) explains how manifests are found and retrieved.*
