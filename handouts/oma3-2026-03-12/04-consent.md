# 04 -- Default-Deny Consent: Privacy That Travels with the Data

---

## The Analogy

Think of a permissions firewall like Little Snitch (or any application firewall). By default, every outbound connection is blocked. Nothing gets through unless you create an explicit rule allowing it. If an app tries to connect to a server you have not approved, the firewall blocks it automatically. There is no "maybe" -- either you allowed it, or it is denied.

Universal Manifest works the same way. Every use of your data is denied by default. A receiving system can read the manifest, but it cannot act on the data unless the manifest explicitly says "this is allowed." No rule means no permission.

---

## Why

When your data moves from one system to another, your privacy preferences should move with it. Today, consent is managed by each platform independently. Platform A knows you allowed voice recording. Platform B has no idea -- it either asks again or assumes it can do whatever it wants. There is no portable mechanism for consent to travel alongside the data it governs.

## What

Universal Manifest uses a **default-deny** consent model with three states:

| State | Meaning | What the consumer does |
|-------|---------|----------------------|
| **allowed** | Explicitly granted | The consumer may use the data for the specified purpose |
| **denied** | Explicitly refused | The consumer must not use the data for the specified purpose |
| **not-set** (absent) | No rule exists | Treated as denied -- the default position is locked |

There is no ambiguity. If a consent key is not present in the manifest, the answer is "no."

Consent rules live inside the manifest document itself. Every downstream system that receives the manifest immediately knows what it is allowed to do -- without calling back to the issuing system, without checking an external consent database, and without displaying a cookie banner.

## How -- Consent in a Manifest

```json
{
  "@context": "https://universalmanifest.net/ns/universal-manifest/v0.1/schema.jsonld",
  "@id": "urn:uuid:6a7b8c9d-2222-4b8d-9d44-9fd2d00a1201",
  "@type": "um:Manifest",
  "manifestVersion": "0.1",
  "subject": "did:example:smart-glasses-user",
  "issuedAt": "2026-02-20T05:10:00Z",
  "expiresAt": "2026-02-21T05:10:00Z",
  "consents": [
    {
      "@type": "um:Consent",
      "name": "ar.recording.faceVisible",
      "value": "allowed"
    },
    {
      "@type": "um:Consent",
      "name": "ar.recording.voiceAllowed",
      "value": "allowed"
    },
    {
      "@type": "um:Consent",
      "name": "ar.profile.autoSharePublic",
      "value": "allowed"
    },
    {
      "@type": "um:Consent",
      "name": "ar.profile.autoShareProfessional",
      "value": "denied"
    }
  ]
}
```

This manifest belongs to a smart glasses user. It says:

- Face recording: **allowed** -- AR systems may record and display this user's face.
- Voice recording: **allowed** -- AR systems may capture and process this user's voice.
- Public profile sharing: **allowed** -- the system may auto-share the public profile.
- Professional profile sharing: **denied** -- the system must not share professional details.

Any consent key not listed (for example, `ar.analytics.biometric`) is treated as **denied**. The system does not need to guess.

### Why consent inside the document matters

**Portability.** When a manifest travels from System A to System B to System C, every system in the chain has the same consent rules. There is no "consent got lost in transit" problem.

**No callback required.** The receiving system does not need to contact the issuing system to check permissions. The consent rules are right there in the document. This enables offline operation and reduces latency.

**Tamper-evident.** In v0.2 manifests, the consent array is covered by the cryptographic signature (see [05 -- Signatures](05-signatures.md)). If someone modifies a consent rule in transit, the signature breaks. The receiving system detects the tampering and rejects the manifest.

---

*Next: [05 -- Signatures](05-signatures.md) explains how manifests are protected against tampering.*
