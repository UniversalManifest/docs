# V-01: The Portable Envelope

**Duration:** 30–45 seconds
**Format:** Motion graphics / animated explainer
**Audience:** First exposure — someone encountering Universal Manifest for the first time.
**Tone:** Clean, confident, modern. Think Stripe or Linear product video.
**Concept:** What a Universal Manifest is — a portable JSON-LD state capsule with a unique ID and built-in expiration.

---

### Scene 1: The Problem (10s)

**Visual:** Three platform icons (social app, enterprise system, IoT device) float on a dark canvas. Between them, tangled lines represent point-to-point API integrations. Data fragments — tiny colored tiles labeled "name," "avatar," "permissions" — fly chaotically between platforms, duplicating and scattering. The tangle grows messier with each connection.

**Narration:** "Every time two systems need to share identity, credentials, or permissions, they build a custom integration. The result: fragile connections and fragmented data."

**On-screen text:** `Fragmented. Duplicated. Fragile.`

---

### Scene 2: The Envelope (15s)

**Visual:** The chaos freezes. A warm glow appears at the center. The scattered data tiles are pulled inward, condensing into a single compact document — a glowing card shape. The card's structure materializes:

- A serial number at the top: `urn:uuid:9b1d...` — the UMID.
- A subject line: `did:key:z6Mki...` — who the manifest is about.
- A timeline bar along the bottom: `issuedAt → expiresAt` — a countdown showing remaining validity.

The card pulses once — it is alive.

**Narration:** "Universal Manifest replaces this with one portable document. A JSON-LD envelope with a unique identifier, a subject, and a built-in expiration. Any system that can parse JSON can consume it. The expiration means edge devices can cache it and know exactly when to stop trusting it — no server check required."

**On-screen text:** `UMID: globally unique lookup key` | `TTL: self-expiring trust window`

---

### Scene 3: The Result (10s)

**Visual:** The three platform icons reappear, now connected by clean, straight beams of light passing through the central manifest card. Each platform reads from the same document. No duplication, no custom wiring. The manifest glows steadily at the center.

The Universal Manifest wordmark appears below. The URL fades in.

**Narration:** "One document. Every system. Portable, time-limited, and ready to go."

**On-screen text:** `universalmanifest.net`

---

## Production Notes

- **Key technical accuracy:** The manifest is a JSON-LD document. The `@context` field provides Linked Data semantics for systems that support it, while remaining valid JSON for those that do not. The UMID is a UUID URN. TTL is defined by `issuedAt` and `expiresAt` timestamps, not a duration field.
- **Visual palette:** Dark background (#0f172a). Manifest card glows warm gold. Platform icons are neutral gray until connected, then accent-colored.
- **Sound design:** Chaos phase has discordant chimes. Condensation moment has a satisfying "snap." Final state has a clean, resolving tone.
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
