# Universal Manifest -- Full Briefing

## Executive Summary

Imagine a Swiss Army Knife for your personal data -- one compact document that carries your identity, credentials, preferences, and permissions between any app, device, or service that needs them. That's Universal Manifest. Instead of every pair of systems inventing a new way to share your information, UM gives them one portable format they all understand. It works offline, expires automatically so stale data can't linger, and nothing gets shared without your explicit permission.

## The Fragmentation Problem

Here is a situation most developers and product teams will recognize. You are building a system, and it needs to know something about a user who comes from another system. Maybe it's their display name. Maybe it's whether they've verified their identity. Maybe it's their device registration, or their privacy preferences, or their role at an organization.

So you do what everyone does: you write a custom integration. You agree on an API, a data shape, an auth flow. It works. Then a third system needs the same information, and you do it all again -- differently, because that system has its own conventions. Then a fourth. Then a tenth. Each integration is its own format, its own handshake, its own maintenance burden.

This is the fragmentation problem, and it's everywhere:

- **Social platforms** each store your profile in a proprietary format. Move to a new one, and you start from scratch.
- **IoT and edge devices** need to know who's authorized and what policies apply, but there's no standard "permission packet" they can all consume.
- **Privacy preferences** are trapped in the system where you set them. The next system you visit has no idea what you consented to.
- **Verification credentials** (proof of age, proof of personhood, professional licenses) have no portable container that works across providers.
- **Offline environments** -- venues, public displays, field operations -- can't call home to verify every claim in real time, so they either trust everything or trust nothing.

The cost isn't just technical. It's organizational (every integration needs coordination), financial (custom work multiplied by every system pair), and human (people lose control of their data because no format carries their preferences alongside their information).

## The Solution: Universal Manifest

Universal Manifest (UM) is a portable JSON-LD document format designed to end this fragmentation. A single manifest carries everything a receiving system needs to know about a subject -- identity references, verified claims, privacy consents, device registrations, and pointers to authoritative data -- in one standardized package.

The key design principles are:

1. **One format, many consumers.** Any system that can parse JSON can read a manifest. Systems that understand JSON-LD get richer semantics for free.
2. **Offline tolerance.** Every manifest has a validity window (`issuedAt` and `expiresAt`). Systems can cache it, use it while offline, and know exactly when to stop trusting it.
3. **Forward compatibility.** Consumers must safely ignore fields they don't recognize. This means new features can be added to the format without breaking existing implementations.
4. **Consent by default.** The permission model is default-deny. Nothing is shared unless the manifest explicitly says so.
5. **Composability.** Manifests are built from modular sections (shards) that can be mixed, matched, and extended for different use cases.

## Core Concepts

Understanding UM requires six concepts. Each one maps to something familiar.

### UMID -- "A Passport Number for Data"

Every manifest has a globally unique identifier, its UMID (Universal Manifest Identifier). Just like a passport number lets any border agent look up your travel record, a UMID lets any system look up the full manifest. The recommended format is a UUID-based URN (`urn:uuid:...`), which can be generated offline without any central registry. You can resolve any UMID through the resolver service at `myum.net/{UMID}`.

### TTL -- "An Expiry Date on a Coupon"

Every manifest carries two timestamps: `issuedAt` (when it was created) and `expiresAt` (when it stops being valid). Think of it like the expiry date on a coupon. After that date, the coupon is worthless -- you don't need to call the store to confirm. This is critical for offline environments: a device with no internet connection can still know when to stop trusting a cached manifest without needing a revocation check.

### Shards -- "Compartments in a Swiss Army Knife"

Shards are the modular sections inside a manifest. Each shard carries a specific slice of data -- a public profile, a device registration, a venue policy, a gaming achievement. They're like the different tools that fold out of a Swiss Army Knife: the knife blade, the screwdriver, the bottle opener. Each one serves a different purpose, and you only open the ones you need. A manifest can carry any number of shards, and consumers pick the ones they understand.

Well-known shard names include `canonicalProfilePointer` (link to a canonical identity source), `publicProfile` (a safe-to-render public projection), `deviceIdentity` (device hardware and capabilities), and `venuePolicy` (venue content rules). But shards are extensible -- you can define your own for any use case.

### Pointers -- "Business Cards, Not Copied Documents"

Pointers are references to data at its authoritative source. Instead of copying someone's entire profile into the manifest, you include a pointer -- a URL where the canonical version lives. It's the difference between photocopying someone's resume and handing out their business card with a link to their portfolio.

This keeps manifests small and avoids the "stale copy" problem. The manifest tells you *where* to find authoritative data; it doesn't try to *be* all the data. Pointer names include `solidPod.creatorCanonical` (link to a Solid Pod), `matrix.userId` (a Matrix messaging identity), and `activityPub.actor` (a fediverse identity).

### Consent -- "Permission Slips That Default to 'No'"

The consent section of a manifest carries explicit permission grants and denials. The model is default-deny: if a consent isn't present, the answer is "no." This is the opposite of how most systems work today, where data is shared by default and you have to opt out.

Each consent entry has a name (like `publicDisplay` or `analytics.proofOfPlay`) and a value indicating whether permission is granted. Consents travel with the manifest, so every system that receives it knows what it's allowed to do -- without calling back to the original system to check.

### Signatures -- "A Notary Stamp on the Document"

In v0.2 (currently in draft), manifests can carry a cryptographic signature that proves the document hasn't been tampered with and was issued by the claimed source. Think of it as a notary stamp: anyone can read the document, but the stamp proves it's authentic.

The v0.2 signature profile uses JCS (JSON Canonicalization Scheme) to create a stable signing input and Ed25519 for the actual cryptographic signature. The design is deliberately modular -- future versions can add additional signature profiles without breaking existing ones, because consumers verify the profiles they support and safely skip unknown ones.

## How It Works End-to-End

The lifecycle of a Universal Manifest follows five stages:

**1. Create.** An issuer (a person, an app, an organization) creates a manifest document. They set the subject, choose a validity window, populate shards with relevant data, set consent flags, and optionally sign the document. The manifest gets a unique UMID.

**2. Publish.** The issuer makes the manifest available. This could mean storing it on the resolver service at `myum.net`, embedding it in a QR code, transmitting it over Bluetooth, or simply saving it to a local file. UM is transport-agnostic -- it doesn't care how the document gets from A to B.

**3. Resolve.** A consumer (another system, device, or app) receives or looks up the manifest. If they have a UMID, they can resolve it through `myum.net/{UMID}`. If they received the manifest directly (via QR code, API call, file transfer), they already have it.

**4. Validate.** The consumer checks the manifest against the spec. Is the structure valid? Is the validity window current (not expired, not issued in the future)? If a signature is present, does it verify? Are the required fields present? Validation can be performed using the published JSON Schema in any language, or using the TypeScript reference implementation which provides ready-made validation functions.

**5. Consume.** The consumer reads the shards, pointers, claims, and consents it understands, ignoring any it doesn't recognize (forward compatibility). It respects the consent flags, follows pointers to canonical data sources if needed, and uses the manifest data for its purpose -- rendering a profile, authorizing access, enrolling a device, or anything else.

## Real-World Scenarios

### Freelance Artist at a Gallery

Alex is a digital artist showing work at Jordan's gallery. Alex's manifest carries a public profile shard (display name, bio, avatar), a `canonicalProfilePointer` to their Solid Pod, a `publicDisplay` consent set to "allowed," and a validity window of 24 hours. Jordan's gallery system scans Alex's manifest, validates it, renders Alex's profile on a public display, and automatically stops showing it when the manifest expires.

### Privacy-Conscious Smart Glasses User

Riley wears smart glasses in a public space. Riley's manifest carries a consent section with `faceVisibility.recording` set to "denied." Other devices in the space that support UM can read Riley's manifest and know not to include Riley's face in recordings or smart glasses overlays -- without Riley having to configure anything in each device separately.

### Cross-Platform Gaming Profile

Sam runs a gaming platform. Players carry manifests with a `gameProfile` shard containing their handle, achievements, and avatar preferences. When a player moves to a different platform that supports UM, their profile comes with them. No re-registration, no lost progress, no API integration between the two platforms.

### Offline Venue Device Enrollment

A public display at a remote venue has intermittent internet. The venue operator creates a manifest for the device with a `deviceIdentity` shard, a `venueAssociation` shard, and a 12-hour validity window. The device caches the manifest locally, operates according to its policies while offline, and knows to stop trusting its authorization after 12 hours without a refresh.

### Proof-of-Personhood Across Providers

A user has verified their personhood through World ID (biometric) and Gitcoin Passport (composite score). Their manifest carries claims from both providers in separate shards. A receiving system can check either or both, depending on its trust requirements, without needing to integrate directly with either provider.

### Portable Professional Credentials

A licensed contractor carries a manifest with a shard containing their license number, issuing authority, and a pointer to the authority's verification endpoint. Any job site system that reads UM can verify the contractor's credentials without building a custom integration with the licensing authority.

## Technical Foundation

UM is built on established standards, not invented from scratch.

**JSON-LD** provides the document structure. Every manifest is valid JSON (any JSON parser can read it) and optionally valid JSON-LD (systems that understand linked data get richer semantics, like unambiguous type definitions via the `@context`). The `@context` points to a published schema at `universalmanifest.net`.

**DIDs (Decentralized Identifiers)** are the recommended format for subject identifiers. A DID like `did:key:z6Mkp...` is a globally unique, self-sovereign identifier that doesn't depend on any central authority. But UM doesn't require DIDs -- any URI works as a subject identifier.

**Ed25519** is the cryptographic algorithm for the v0.2 signature profile. It's fast, widely supported, and produces compact signatures -- important for constrained environments like edge devices and public displays.

**JCS (JSON Canonicalization Scheme, RFC 8785)** provides deterministic JSON serialization for the signature profile. Before signing, the manifest is canonicalized using JCS so that the same logical document always produces the same byte sequence, regardless of whitespace or key ordering.

**JSON Schema** provides structural validation. The spec includes JSON Schema files for both v0.1 and v0.2 that can be used with any JSON Schema validator to check whether a document conforms to the manifest structure.

## Adoption Path

UM is designed for progressive adoption. You don't have to buy into the entire ecosystem at once.

**Level 1 -- Parse it.** Your system can read a manifest using any JSON parser. Extract the fields you care about, ignore the rest. This requires zero dependencies beyond your language's JSON library.

**Level 2 -- Validate it.** Use the published JSON Schema to validate manifest structure, check validity windows, and enforce required fields. The TypeScript reference implementation (`universal-manifest` on npm) is one option, but any JSON Schema validator works.

**Level 3 -- Consume shards.** Read well-known shard names from the registry and use the data they carry. This is where UM starts replacing custom integrations.

**Level 4 -- Issue your own.** Create manifests for your users, devices, or organizations. Publish them to the resolver at `myum.net` or distribute them through your own channels.

**Level 5 -- Sign and verify.** Adopt the v0.2 signature profile to issue tamper-proof manifests and verify the authenticity of manifests you receive.

## Competitive Positioning

UM exists in a landscape with other standards for portable identity and credentials. Here's how it relates to them.

**W3C Verifiable Credentials (VCs):** VCs are a well-established standard for issuing and verifying individual claims. UM is not a replacement for VCs -- it's a *container* that can carry VCs as claims within shards. Think of a VC as a single stamp in your passport; UM is the passport itself.

**DIDComm:** DIDComm is a messaging protocol for exchanging data between DID-based systems. UM is a document format, not a messaging protocol. A DIDComm message could carry a UM manifest as its payload. They're complementary layers.

**Solid Pods:** Solid provides decentralized data storage with fine-grained access control. UM manifests use pointers to reference data stored in Solid Pods. Rather than competing, UM acts as the portable summary layer while Solid provides the canonical storage.

**OpenID Connect / OAuth tokens:** OIDC tokens carry authentication state. UM manifests carry a broader set of portable state (identity + credentials + preferences + consent + device registrations). A UM manifest might include an OIDC-derived claim, but it serves a different architectural purpose.

The key differentiator is that UM is a **portable state document**, not just a credential, not just an auth token, not just a data store. It's the one document that holds enough context for a receiving system to act -- even offline, even without prior integration.

## Frequently Asked Questions

**Q: Does UM require blockchain or cryptocurrency?**
No. UM is a document format that works with any identifier scheme and any transport. Some integration lanes explore blockchain-based DIDs (like `did:chia`), but these are optional extensions, not requirements.

**Q: How big is a typical manifest?**
A minimal manifest is under 300 bytes of JSON. A manifest with several shards and pointers is typically 1-3 KB. The format is designed to be small enough for QR codes, Bluetooth transmission, and edge-device caching.

**Q: What happens when a manifest expires?**
Consumers must reject expired manifests. The issuer creates a new manifest with a fresh validity window. There is no renewal mechanism -- expired means expired, and a new document must be issued.

**Q: Can I use UM without JSON-LD?**
Yes. Every manifest is valid JSON. The `@context`, `@id`, and `@type` fields use JSON-LD conventions, but you can parse and use the document with a plain JSON parser. JSON-LD awareness is optional and additive.

**Q: Is UM a finished standard?**
v0.1 is stable and has production infrastructure live (resolver, documentation site, published schemas, and a TypeScript reference implementation). v0.2, which adds the signature profile, is in draft. The project follows an incremental approach: ship what works, add capabilities in future versions.

**Q: Who controls the spec?**
The spec is open source under the Apache-2.0 license. Development happens in the public GitHub repository, and contributions are welcome per the project's contributing guidelines.

## Links and Resources

- **Specification (v0.1):** [spec/v0.1/README.md](../../spec/v0.1/README.md)
- **Specification (v0.2 draft):** [spec/v0.2/README.md](../../spec/v0.2/README.md)
- **Code examples:** [examples/code/README.md](../../examples/code/README.md)
- **Example manifests:** [examples/v0.1/](../../examples/v0.1/)
- **Documentation site:** [universalmanifest.net](https://universalmanifest.net)
- **Resolver service:** [myum.net](https://myum.net)
- **GitHub repository:** [github.com/grigb/universal-manifest](https://github.com/grigb/universal-manifest)
- **TypeScript reference implementation:** `universal-manifest` on npm
- **License:** Apache-2.0
