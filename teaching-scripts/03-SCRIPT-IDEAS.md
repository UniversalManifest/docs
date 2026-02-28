# 03 -- Teaching Script Ideas

## Overview

This document contains 20 teaching script concepts organized by difficulty level. Each script uses the Capsule-Pod character (see 01-ICONIC-REPRESENTATION.md) and follows the scene format defined in 02-SCRIPT-FORMAT.md.

Scripts build on each other. A viewer who watches the beginner scripts first will have the visual vocabulary needed to understand the intermediate and advanced ones.

---

## Category A: "What Is This Thing?" (Beginner -- Introducing the Pod)

### TS-001: What Is a Universal Manifest?

**Pitch**: The very first encounter with the Capsule-Pod. A small point of light forms into the pod shape. The viewer learns that this shape represents a "portable state capsule" -- a single document that carries identity, claims, and permissions between any two systems. No jargon. No JSON. Just the shape, the name, and the idea that it travels.

**Pod journey**: Created from nothing at center screen. Rests while being named. Slides between two generic system icons. Arrives and gets verified (green glow). Rests as end card.

**Duration**: 30s
**Complexity**: Simple
**Concepts**: `manifest-envelope`, `portable-state`

---

### TS-002: Inside the Pod

**Pitch**: The pod from TS-001 returns, but now it opens up to reveal its internal structure. The viewer learns that a manifest has layers: a header (who it is, when it was made), an integrity layer (signatures), and a payload (shards, claims, consents, pointers). Each layer is shown as a colored band inside the pod. The viewer learns the word "envelope" without needing to know JSON-LD.

**Pod journey**: Starts resting at center. The shell becomes semi-transparent. Layers are revealed from outside in: header (blue), integrity (amber), payload (green). Each layer gets a one-word label. The shell becomes opaque again -- the pod is a single unit, but now the viewer knows it has structure.

**Duration**: 30s
**Complexity**: Simple
**Concepts**: `manifest-envelope`, `shards`, `claims`, `consents`, `pointers`

---

### TS-003: The Expiration Clock

**Pitch**: Every manifest has a built-in expiration time. This script shows the pod with a visible countdown timer. As time passes, the pod's glow gradually shifts from blue to amber to red. When the timer hits zero, the pod's shell cracks and dissolves. The viewer learns that manifests are never permanent -- they are deliberately ephemeral. A new pod can be issued to replace the old one, but stale state is never trusted.

**Pod journey**: Starts resting with a timer overlay. Transitions through color states as time passes. Reaches zero and enters the expired/shattered state. A new pod forms beside the old one's remains -- fresh, valid, ready.

**Duration**: 30s
**Complexity**: Simple
**Concepts**: `ttl-expiry`, `manifest-envelope`

---

### TS-004: Who Issued This?

**Pitch**: Every manifest has an issuer who created and signed it. This script shows a character (the issuer) crafting a pod -- placing data inside, sealing the shell, and applying a signature (visualized as a wax-seal gesture on the pod's surface). The viewer learns that manifests are not anonymous -- they are authored and accountable. The signed pod is then handed to a traveler who carries it forward.

**Pod journey**: The issuer character assembles the pod (being-created state). The shell wraps around the payload. The issuer applies a seal (a glowing mark on the shell). The pod transitions to resting state and is passed to a messenger character.

**Duration**: 30s
**Complexity**: Simple
**Concepts**: `manifest-envelope`, `signature-verification`

---

## Category B: "Watch It Travel" (Beginner/Intermediate -- Portability)

### TS-005: Crossing the Boundary

**Pitch**: The pod leaves one system (shown as a walled city with a gate) and arrives at another. At the gate of the second city, a guard inspects the pod -- checking the seal, reading the header, confirming it has not expired. The gate opens, and the pod enters. The viewer learns that manifests cross system boundaries by being self-describing and self-verifying. No shared database. No bilateral API integration. Just the pod and its contents.

**Pod journey**: Starts inside System A's walls. Exits through the gate. Travels across open space (in-transit glow). Arrives at System B's gate. The guard (a scanner beam) inspects the pod. The gap illuminates green. The gate opens. The pod enters.

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `portable-state`, `cross-system-handoff`, `signature-verification`

---

### TS-006: The Resolver -- Finding a Manifest by Name

**Pitch**: Someone has a manifest ID (a UMID) but not the manifest itself. They visit the resolver (myum.net), hand over the ID, and receive the full pod in return. The viewer learns that every manifest has a unique address and can be looked up from anywhere. The resolver is like a phone book for manifests.

**Pod journey**: The pod does not appear at first. A character holds a slip of paper labeled "UMID." They approach the resolver (a glowing tower/kiosk). They hand over the slip. The resolver searches briefly (a spinning animation), then produces the pod. The character receives the pod, and it glows in their hands.

**Duration**: 30s
**Complexity**: Simple
**Concepts**: `resolution`

---

### TS-007: One Pod, Three Readers

**Pitch**: A single pod arrives at a crossroads where three different systems wait: a social platform, a venue display, and a spatial computing engine. Each system picks up the pod, reads it, and sees something different -- the social platform sees the profile shard, the venue display sees the public capsule shard, the spatial engine sees the spatial anchors shard. But they all read the same pod. The viewer learns about projection: one manifest, many views.

**Pod journey**: Arrives at center from the left. Three paths diverge to three systems. The pod is "projected" through a prism shape at the crossroads -- three colored beams emerge, each carrying a labeled shard to its destination system. The pod remains at the center, unchanged.

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `projection`, `shards`, `shard-composition`

---

### TS-008: Handing Off Between Worlds

**Pitch**: A character exists in World A (a blue-tinted environment). They carry their pod to the edge of World A, where it meets World B (a green-tinted environment). The pod crosses the boundary. In World B, the pod is verified and the character's identity is recognized -- their name, their permissions, their preferences all transfer seamlessly. The viewer learns that Universal Manifest enables identity portability between completely separate platforms.

**Pod journey**: Starts with the character in World A. The pod is visible at the character's side. They approach the boundary (a shimmering membrane). The pod passes through the membrane (a brief gold flash at the boundary). In World B, the pod is scanned and verified. The character's profile appears in World B's style, derived from the pod's contents.

**Duration**: 60s
**Complexity**: Medium
**Concepts**: `portable-state`, `cross-system-handoff`, `projection`

---

## Category C: "Can You Trust It?" (Intermediate -- Verification and Integrity)

### TS-009: The Signature Check

**Pitch**: A deep dive into what verification looks like. The pod arrives at a system. The system performs three checks, shown as three sequential scanning passes: (1) Is the structure valid? (header check -- blue pulse), (2) Has it expired? (TTL check -- amber pulse), (3) Is the signature genuine? (signature check -- green pulse). All three pass, and the pod is accepted. Then the same sequence plays again with a tampered pod -- the third check fails (red crack), and the pod is rejected.

**Pod journey**: First pass: arrives, three checks pass, accepted (green glow). Second pass: a different pod arrives (visually identical but with a subtle visual flaw), two checks pass, third check fails (red crack in shell), rejected (shatter animation).

**Duration**: 60s
**Complexity**: Medium
**Concepts**: `signature-verification`, `tamper-detection`, `ttl-expiry`

---

### TS-010: Offline Verification -- No Network Needed

**Pitch**: A pod arrives at a system that has no internet connection (shown by a crossed-out wifi symbol and a disconnected cable). The viewer expects verification to fail -- but it does not. The system reads the public key embedded in the pod itself (`publicKeySpkiB64`), uses it to verify the signature, and accepts the manifest. The viewer learns that UM verification works entirely locally when the key material is embedded.

**Pod journey**: Arrives at an isolated system (no network indicators). The system attempts a network call (a dashed line reaches out and hits a wall). But then it reads the pod's own key material (a key icon floats out of the pod's payload area). The system uses the key to verify the signature (green glow). The pod is accepted.

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `offline-verification`, `signature-verification`

---

### TS-011: The Tampered Manifest

**Pitch**: A villain (a shadowy hand or a glitch effect) intercepts a pod in transit and modifies its contents -- changing a claim value, altering a consent setting. The pod arrives at its destination looking normal. But during verification, the signature check fails. The gap between shell and payload flashes red. A crack appears in the shell. The pod is rejected. The viewer learns that any modification to any field invalidates the signature -- tamper detection is total.

**Pod journey**: Created and launched in-transit. Intercepted mid-journey by a malicious actor (a brief red glitch overlay). Arrives at the destination. The system scans it. Structure check passes. TTL check passes. Signature check fails (dramatic red flash, crack in shell). The pod shatters. A callout explains: "Any change breaks the seal."

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `tamper-detection`, `signature-verification`

---

### TS-012: Revocation -- Taking It Back

**Pitch**: An issuer creates a pod and sends it into the world. Later, the issuer decides the manifest should no longer be trusted (perhaps the user's permissions changed, or the key was compromised). The issuer publishes a revocation notice. When the pod arrives at a system that checks for revocation, the system queries the revocation endpoint, discovers the manifest is revoked, and rejects it -- even though the signature is still technically valid. The viewer learns that manifests can be invalidated after issuance.

**Pod journey**: Created and sent. Passes through several systems successfully (green glow at each). The issuer then posts a revocation (a red X appears at the issuer's location). The pod arrives at the next system. Signature check passes. But then a revocation check runs (a query arrow goes to the revocation endpoint). The revocation is confirmed. The pod transitions to expired state and is rejected.

**Duration**: 60s
**Complexity**: Complex
**Concepts**: `revocation`, `signature-verification`

---

## Category D: "It Is More Than It Looks" (Intermediate/Advanced -- Composition)

### TS-013: Shards -- The Compartments Inside

**Pitch**: The pod opens to reveal multiple compartments (shards), each a different color and labeled with a name: "publicProfile," "deviceRegistration," "crossWorldProfile." Each shard is a self-contained package that can be read independently. The viewer learns that shards are the composition mechanism -- a single manifest can carry data for many different purposes without those purposes conflicting.

**Pod journey**: Starts resting. Shell becomes transparent. Inside, multiple colored blocks (shards) are visible, neatly stacked. Each block rises and gets labeled. Then each block briefly expands to show its contents (a miniature data display). The blocks return to their stack. The shell becomes opaque again. The pod is a single document, but it contains multitudes.

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `shards`, `shard-composition`

---

### TS-014: Pointers -- The References That Reach Out

**Pitch**: The pod arrives at a system. The system reads the pod and finds a pointer: a URL reference to an external data source. Instead of containing the full data, the pod points to where the authoritative data lives. The system follows the pointer (an arrow extending from the pod to a distant server) and retrieves the full data. The viewer learns that pointers keep manifests lightweight while enabling access to rich external data.

**Pod journey**: Arrives at a system. The system opens the pod (projection state). Inside, instead of a full data block, there is a small arrow icon labeled "pointer." The arrow extends outward from the pod, crossing the scene to reach a remote server. The server sends back a data package that the system receives. The pod stays small; the data source is large.

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `pointers`, `manifest-envelope`

---

### TS-015: Consent Gates -- The Permissions Layer

**Pitch**: A pod arrives at a system that wants to do three things: display the user's profile (allowed), record their face (denied), and share their location (restricted). For each action, the system checks the pod's consent keys. A green gate opens for "allowed." A red barrier blocks "denied." An amber gate partially opens for "restricted" (with conditions). The viewer learns that consent is structural -- it is part of the manifest, not an afterthought.

**Pod journey**: Arrives at a system. Three paths extend from the pod to three actions. Each path has a gate. The system reads the consent keys (a magnifying glass on the pod's consent section). Gate 1 opens green. Gate 2 slams shut red. Gate 3 opens partway amber. The viewer sees that the manifest itself controls what the system can do.

**Duration**: 45s
**Complexity**: Medium
**Concepts**: `consents`, `consent-enforcement`

---

### TS-016: Forward Compatibility -- The Unknown Field

**Pitch**: A pod from the future arrives at a system built today. The pod contains fields the system has never seen before (labeled with "???" icons). The system parses the pod, reads the fields it understands, and simply ignores the unknown fields. Everything works. The viewer learns the forward-compatibility rule: consumers must safely ignore unknown fields. This is what allows the standard to evolve without breaking existing implementations.

**Pod journey**: A pod arrives with some familiar labels (blue) and some unfamiliar labels (grey with "?" marks). The system scans the pod. It reads the familiar fields (they light up blue). It encounters the unknown fields (they pulse grey briefly). The system shrugs (a tiny animation) and proceeds. Everything works. A callout: "Unknown fields are preserved, not rejected."

**Duration**: 30s
**Complexity**: Simple
**Concepts**: `forward-compatibility`

---

## Category E: "Real World" (Advanced -- Integration Lane Scenarios)

### TS-017: Social Profile -- One Manifest, Every Platform

**Pitch**: A creator named Jules publishes a single manifest. That manifest is picked up by Mastodon (which reads the ActivityPub actor pointer), by a venue display screen (which reads the publicProfile shard), and by a web profile page (which reads the full profile shard and renders it as HTML). Three completely different systems, three completely different projections, one single manifest. The viewer understands multi-platform identity.

**Pod journey**: Jules creates the pod (being-created). The pod is published. Three systems approach: Mastodon (elephant icon), a venue display (screen icon), and a web browser (globe icon). Each system passes the pod through a prism. Each prism produces a different colored beam carrying a different shard/pointer. Each system renders its own view of Jules's identity.

**Duration**: 60s
**Complexity**: Complex
**Concepts**: `projection`, `shards`, `pointers`, `cross-system-handoff`

---

### TS-018: Smart Glasses -- Consent in Real Time

**Pitch**: Alex walks into a conference wearing smart glasses. Other attendees' glasses detect Alex and fetch Alex's manifest. Alex's consent keys say: face recording denied, professional profile public, voice capture denied. The glasses respond in real time: Alex's face is blurred in the recording feed, their professional badge appears in the AR overlay, and voice capture is muted. The viewer sees consent enforcement as a live, visual process.

**Pod journey**: Alex's pod floats beside the character. Other glasses (represented as small scanner icons) approach. They fetch the pod. They read the consent keys. Three visual outcomes play simultaneously: face blurred (red overlay on face area), badge appears (green nameplate materializes), voice muted (red X on microphone icon). The pod is never modified -- it just controls what others can do.

**Duration**: 60s
**Complexity**: Complex
**Concepts**: `consents`, `consent-enforcement`, `cross-system-handoff`

---

### TS-019: IoT Device -- The Venue Display

**Pitch**: A cafe enrolls a display device (an NVIDIA Shield). The venue edge server issues a manifest for the device: its identity, capabilities, content policy, and operational pointers. The display receives the manifest, caches it, and uses it to determine what content to show and what to block. When the venue updates the manifest (new policy), a push signal triggers the display to fetch the new version. The old manifest expires via TTL.

**Pod journey**: The venue server creates a device pod (being-created). The pod travels to the display device. The display caches the pod (a copy animation). The pod controls what the display shows (content cards appear/disappear based on policy shards). Time passes. The venue creates a new pod. A signal pushes to the display. The display fetches the new pod. The old pod's TTL expires (amber to red, dissolve). The new pod takes over.

**Duration**: 90s
**Complexity**: Complex
**Concepts**: `device-enrollment`, `ttl-expiry`, `claims`, `pointers`, `cross-system-handoff`

---

### TS-020: Metaverse -- Crossing Virtual Worlds

**Pitch**: Nova exists in World A with an avatar, inventory, reputation, and social graph. Nova wants to move to World B. Their manifest carries a cross-world profile shard listing all supported worlds, plus pointers to avatar data, inventory, and social connections. World B resolves the manifest, verifies the signature, reads the cross-world profile shard, imports Nova's reputation, restores inventory references, and applies consent gates. Nova appears in World B with their identity intact.

**Pod journey**: Nova's pod is visible in World A (a blue-tinted environment with the character's avatar). Nova approaches the world boundary. The pod travels through a portal (a shimmering membrane between worlds). World B (green-tinted) receives the pod. Verification runs (green glow). The cross-world shard is read. The prism effect shows: avatar data flows to the rendering engine, inventory data flows to the item system, social graph flows to the friends list. Nova materializes in World B fully formed.

**Duration**: 90s
**Complexity**: Complex
**Concepts**: `cross-system-handoff`, `shards`, `pointers`, `projection`, `signature-verification`, `consent-enforcement`

---

## Summary Table

| ID | Title | Category | Duration | Complexity | Key Concepts |
|----|-------|----------|----------|------------|--------------|
| TS-001 | What Is a Universal Manifest? | A | 30s | Simple | envelope, portability |
| TS-002 | Inside the Pod | A | 30s | Simple | envelope, shards, claims |
| TS-003 | The Expiration Clock | A | 30s | Simple | TTL, expiry |
| TS-004 | Who Issued This? | A | 30s | Simple | envelope, signatures |
| TS-005 | Crossing the Boundary | B | 45s | Medium | portability, handoff, verification |
| TS-006 | The Resolver | B | 30s | Simple | resolution |
| TS-007 | One Pod, Three Readers | B | 45s | Medium | projection, shards |
| TS-008 | Handing Off Between Worlds | B | 60s | Medium | portability, handoff, projection |
| TS-009 | The Signature Check | C | 60s | Medium | verification, tamper, TTL |
| TS-010 | Offline Verification | C | 45s | Medium | offline verification |
| TS-011 | The Tampered Manifest | C | 45s | Medium | tamper detection |
| TS-012 | Revocation | C | 60s | Complex | revocation, verification |
| TS-013 | Shards -- The Compartments | D | 45s | Medium | shards, composition |
| TS-014 | Pointers -- The References | D | 45s | Medium | pointers |
| TS-015 | Consent Gates | D | 45s | Medium | consents, enforcement |
| TS-016 | Forward Compatibility | D | 30s | Simple | forward compatibility |
| TS-017 | Social Profile | E | 60s | Complex | projection, shards, pointers |
| TS-018 | Smart Glasses | E | 60s | Complex | consents, enforcement |
| TS-019 | IoT Device | E | 90s | Complex | device enrollment, TTL, claims |
| TS-020 | Metaverse Crossing | E | 90s | Complex | handoff, shards, projection |

---

## Suggested Viewing Order

**First-time viewer (5 minutes)**:
1. TS-001 -- What Is a Universal Manifest? (30s)
2. TS-002 -- Inside the Pod (30s)
3. TS-005 -- Crossing the Boundary (45s)
4. TS-009 -- The Signature Check (60s)
5. TS-007 -- One Pod, Three Readers (45s)

**Deep dive (15 minutes)**: All 20 scripts in order, TS-001 through TS-020.

**Executive overview (2 minutes)**:
1. TS-001 -- What Is a Universal Manifest? (30s)
2. TS-007 -- One Pod, Three Readers (45s)
3. TS-017 -- Social Profile (60s)

---

## Future Script Ideas (Not Yet Developed)

These ideas are noted for future development but do not yet have full pitches:

- **TS-021**: Healthcare Consent Capsule -- patient consent traveling between hospitals
- **TS-022**: Supply Chain Provenance -- a coffee bag's manifest tracing its origin
- **TS-023**: AI Agent Authorization -- an AI agent presenting its capability manifest
- **TS-024**: Chia DID/VC -- on-chain credential verification
- **TS-025**: OMATrust Attestation -- trust scoring and lifecycle management
- **TS-026**: Proof of Personhood -- multi-provider verification coexisting in one manifest
- **TS-027**: The Full Lifecycle -- creation, travel, verification, projection, expiration, reissuance
- **TS-028**: Digital Twin -- an industrial device publishing its operational state
- **TS-029**: Education Credentials -- student credential portability
- **TS-030**: DeFi KYC -- portable compliance across protocols
