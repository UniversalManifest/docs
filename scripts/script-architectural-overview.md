# Universal Manifest: Architectural Overview (Data Structures & File Formats)

**Duration:** 3–5 minutes
**Audience:** Technical Leadership, Architects, System Integrators (e.g., Alfred Tom).
**Objective:** Explain the Universal Manifest (UM) as a standardized architectural component—focusing on its composite stack, data structures, and file formats—independent of any specific implementation like PeerMesh.
**Tone:** Authoritative, clear, and focused on systems integration and data portability.

---

### Slide 1: The Portability Problem
**Visual:** A diagram showing isolated databases (silos) representing different platforms (social, enterprise, IoT). Arrows try to connect them, creating a messy, tangled web of point-to-point API integrations.
**Speaker Notes:**
"Today, every time two systems need to exchange state—whether that's user identity, verified credentials, or privacy preferences—they build a custom integration. The result is a fragile, tightly coupled web of APIs. Universal Manifest (UM) introduces a standardized, portable envelope to solve this data fragmentation. It is not a new database or a new protocol; it is a portable state document that acts as a secure transit layer between systems."

### Slide 2: The Universal Manifest File Format
**Visual:** A clean code snippet showing the root structure of a Universal Manifest JSON document. Highlighting the `@context`, `id`, `issuedAt`, and `expiresAt` fields.
**Speaker Notes:**
"At its core, a Universal Manifest is simply a JSON-LD document. If a system can parse JSON, it can consume a manifest.
For systems that understand Linked Data, the JSON-LD `@context` provides rich, unambiguous semantics.
Every manifest has a globally unique identifier (typically a UUID URN) and built-in validity timestamps: 'issued at' and 'expires at'. This time-to-live (TTL) mechanism is critical. It makes UM offline-tolerant. A consuming system or edge device can cache the manifest and know exactly when to stop trusting it, without needing to ping a central server for revocation checks."

### Slide 3: The Data Structure (Shards & Pointers)
**Visual:** An exploded view of the manifest document. The "Envelope" opens up to reveal modular "Shards" (e.g., `publicProfile`, `deviceIdentity`). A magnifying glass hovers over a "Pointer" showing a URL instead of raw data.
**Speaker Notes:**
"The internal data structure is highly modular, organized into what we call 'Shards'. Think of Shards as functional compartments—one shard might carry a public profile, another a venue policy, and another a gaming achievement.
Crucially, UM relies heavily on 'Pointers'. Instead of copying a 50-megabyte 3D avatar or an entire database history into the manifest, it includes a URI pointing to the authoritative source. This keeps the file size extremely lightweight—typically 1 to 3 kilobytes—making it easily transportable via API, Bluetooth, or even a QR code."

### Slide 4: Default-Deny Consent Model
**Visual:** A lock icon next to data fields. A toggle switch flips from 'Red' (Denied) to 'Green' (Allowed). The visual underscores that fields are locked by default.
**Speaker Notes:**
"In traditional systems, data is often shared by default. The UM architecture flips this with a 'Default-Deny' consent model. The manifest carries a dedicated consent structure. If a specific permission isn't explicitly granted within the manifest, the receiving system treats it as denied. Because this consent data travels inside the envelope itself, downstream systems instantly know what they are allowed to do with the data, ensuring privacy compliance is portable and embedded at the data-structure level."

### Slide 5: Integrity and Signatures (v0.2)
**Visual:** The JSON document is processed through a 'JCS Canonicalization' filter, then stamped with an 'Ed25519 Signature'.
**Speaker Notes:**
"For security and trust, we have to know the data hasn't been tampered with in transit. In the v0.2 specification, manifests support cryptographic signatures. We use JSON Canonicalization Scheme (JCS) to ensure the data serializes deterministically, and then sign it using Ed25519. Because the signature profiles are modular, validating systems can verify the profiles they support and safely ignore unknown ones, adhering to our strict forward-compatibility rules."

### Slide 6: The Composite Stack Architecture
**Visual:** A layered architectural diagram:
1. **Storage/Registry** (Solid Pods, Databases)
2. **Transit/State Envelope** (Universal Manifest)
3. **Execution/Runtime** (Web Apps, Native Clients, Spatial Engines)
**Speaker Notes:**
"To understand how Universal Manifest fits into your systems, view it as part of a 'Composite Stack'. UM is the Transit Layer. It doesn't replace your active runtime, and it doesn't replace your canonical storage. Instead, it bridges them. It securely carries identity, pointers, and consents from the storage layer into the execution layer. Whether you are integrating it into an interoperable web platform or an enterprise identity access system, UM is the standardized envelope that makes the handover seamless and secure."

---
**Production Note:**
- This script is completely decoupled from PeerMesh-specific implementations. It focuses purely on standardizing data exchange formats, making it highly applicable for standards bodies and architectural integration discussions.
