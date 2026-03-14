# 03 -- Facets and Pointers: Modular Data Architecture

---

## The Analogy

Think of a filing folder with labeled tabs. One tab says "Public Profile." Another says "Device Registration." A third says "Game Profile." Each tab holds a different category of information. You can add new tabs without reorganizing the folder. Someone looking at the folder reads the tabs they care about and skips the rest.

Now imagine one of those tabs does not contain a full document -- it contains a business card that says "for my full resume, visit this URL." That is the difference between a **facet** (data in the folder) and a **pointer** (a reference to data that lives somewhere else).

---

## Why

A manifest needs to carry different kinds of data for different purposes -- a social profile for a social platform, device credentials for an IoT system, an avatar reference for a metaverse world. Cramming everything into a flat structure creates bloat and makes the manifest hard to extend. And embedding large assets (like 3D avatar meshes) directly would make the document too large to transmit efficiently.

## What

Universal Manifest solves this with two mechanisms:

**Facets** are named, modular data compartments inside the manifest. Each facet carries a specific slice of data. Well-known names exist (`publicProfile`, `deviceRegistration`, `crossWorldProfile`), but any adopter can define domain-specific facets for their use case. Consumers read the facets they understand and safely ignore the rest. This ensures forward compatibility.

**Pointers** are URIs that reference external authoritative data. Instead of embedding a 50 MB 3D avatar mesh into the manifest, include a pointer to where the avatar lives at its canonical source. The manifest stays small. The external resource stays under its owner's control.

## How -- A Manifest with Facets

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
        "description": "NVIDIA Shield TV Pro enrolled to venue edge"
      }
    }
  ]
}
```

Each facet has a `name` (what kind of data it carries) and an `entity` (the data itself). The second facet also has a `ref` -- a URL pointing to the device's canonical registration at an external source.

## How -- A Manifest with Pointers

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.2/schema.jsonld",
  "@id": "urn:uuid:55555555-5555-4555-8555-555555555555",
  "@type": "um:Manifest",
  "manifestVersion": "0.2",
  "subject": "did:example:creator-bob",
  "issuedAt": "2026-02-27T00:00:00.000Z",
  "expiresAt": "2026-02-28T00:00:00.000Z",
  "pointers": [
    {
      "@type": "um:Pointer",
      "rel": "canonical",
      "href": "https://example.pod.provider/bob/profile.jsonld"
    },
    {
      "@type": "um:Pointer",
      "rel": "avatar",
      "href": "https://cdn.example.com/avatars/bob/mesh.glb"
    },
    {
      "@type": "um:Pointer",
      "rel": "social",
      "href": "https://example.social/users/bob"
    }
  ]
}
```

The pointer-first design keeps manifests lightweight -- typically **1-3 KB**. A 50 MB avatar is a 60-byte pointer. A social graph on a data pod is a 70-byte pointer. The manifest is small enough for QR codes, Bluetooth, NFC, or edge-device caching, regardless of how much data it references.

### Key design properties

**Extensible.** Anyone can define new facet names for their domain. A gaming platform defines `gameProfile`. A healthcare system defines `patientSummary`. The manifest format does not need to change.

**Forward-compatible.** Consumers that encounter unknown facets preserve them without rejection. A system built today will not break when new facet types appear tomorrow.

**Separation of data and reference.** Facets carry data. Pointers reference data. Both are covered by the manifest's signature (see [05 -- Signatures](05-signatures.md)), so changing either invalidates the integrity proof.

---

*Next: [04 -- Consent](04-consent.md) explains how privacy rules travel inside the manifest.*
