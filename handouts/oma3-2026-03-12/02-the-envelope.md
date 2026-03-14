# 02 -- Universal Manifest: The Portable Document

---

## The Analogy

A passport is a portable document that carries your identity. It is issued by an authority. It has a photo, a unique number, and an expiration date. Any border agent in any country can read it because the format is standardized. You carry it with you. It is yours.

Universal Manifest is the digital equivalent. It is a standardized JSON-LD document that carries identity, credentials, preferences, and consent rules. Any system that can parse JSON can read it. The document belongs to the subject it describes.

---

## Why

Digital systems need to exchange user state -- identity, preferences, credentials, consent -- but no standard format exists for bundling all of these into a single portable document. Each platform invents its own, and interoperability suffers.

## What

Universal Manifest (UM) is an open specification that defines a portable JSON-LD document format. Each manifest is a self-contained document with:

- A globally unique identifier (the **UMID**)
- A subject (who or what the document describes)
- A validity window (when the document can be trusted)
- Modular data compartments for any kind of state

Any system that can parse JSON can consume a manifest. Systems that understand JSON-LD get richer, unambiguous semantics through the `@context`.

## How -- The Minimal Manifest

This is the smallest valid Universal Manifest. It is approximately 300 bytes:

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld",
  "@id": "urn:uuid:11111111-1111-4111-8111-111111111111",
  "@type": "um:Manifest",
  "manifestVersion": "0.2",
  "subject": "did:example:alice",
  "issuedAt": "2026-02-17T00:00:00.000Z",
  "expiresAt": "2026-02-18T00:00:00.000Z",
  "facets": []
}
```

### What each field means

| Field | Purpose |
|-------|---------|
| `@context` | Points to the JSON-LD vocabulary. Tells consumers how to interpret every term in the document. |
| `@id` | The **UMID** -- a UUID-based URN (`urn:uuid:...`) that identifies this manifest globally. No central registry is required to generate one. |
| `@type` | Declares this document as a Universal Manifest. |
| `manifestVersion` | The spec version (`"0.1"` or `"0.2"`). Consumers use this to select the correct validation rules. |
| `subject` | Who or what this manifest describes. Uses a DID or URI. This field answers: "whose data is this?" |
| `issuedAt` | When the manifest was created. ISO 8601 timestamp. |
| `expiresAt` | When the manifest stops being valid. This is the **TTL** -- the built-in expiration. After this timestamp, consumers must reject the document without needing to call home for a revocation check. |
| `facets` | The modular data compartments (covered in the next document). |

### Key design properties

**Self-contained.** The manifest carries everything a consumer needs to identify the subject, check validity, and determine trust. No external session, token, or API call is required after the initial fetch.

**Offline-tolerant.** The `expiresAt` timestamp means a device can cache the manifest and operate independently until expiration. This is critical for edge devices, smart glasses, and environments with intermittent connectivity.

**Transport-agnostic.** The UMID is a string. It can travel via HTTP, QR code, NFC tap, Bluetooth beacon, or printed on a business card. The manifest format does not depend on how it was delivered.

---

*Next: [03 -- Facets and Pointers](03-facets-and-pointers.md) explains how data is organized inside the manifest.*
