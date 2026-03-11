# V-05: Manifest Resolution

**Duration:** 30–45 seconds
**Format:** Motion graphics / animated explainer
**Audience:** Developers, integrators, and anyone wondering how manifests are discovered and delivered.
**Tone:** Technical but accessible, clean, confident.
**Concept:** How the resolver at myum.net delivers manifests by UMID from anywhere — publish once, fetch from any system.

---

### Scene 1: Publishing (12s)

**Visual:** Alex holds their Universal Manifest card. They walk toward a secure vault — an elegant structure labeled `myum.net`. The vault has a slot. Alex places the manifest into the slot. The vault door closes with a clean mechanical sound.

On the outside of the vault, the UMID illuminates: `urn:uuid:9b1d...`. A small QR code appears beside it. The manifest is now registered and retrievable.

A status indicator glows green: "Published."

**Narration:** "Alex publishes their manifest to the resolver — a lookup service at myum.net. The manifest is stored and indexed by its unique identifier, the UMID. Published once, available to any authorized system."

**On-screen text:** `Publish to myum.net → indexed by UMID`

---

### Scene 2: Resolving (15s)

**Visual:** Cut to a different location. Jordan sits at a terminal. They type the UMID into a search interface: `urn:uuid:9b1d...`. Alternatively, they scan a QR code with a device.

A request beam travels across the screen to the vault. The vault opens. A fresh copy of the manifest appears on Jordan's screen. The TTL bar at the bottom is full — this is the latest version. A small label: "Last updated 12 minutes ago."

Meanwhile, a third system — an app on Sam's phone — also fetches the same UMID. Same manifest, same version, different consumer.

**Narration:** "From anywhere, any system can fetch the manifest by its UMID. Jordan types it in at a gallery terminal. Sam's app fetches it on a phone. Both get the same document — always the latest version. The resolver handles the lookup; the manifest handles the trust."

**On-screen text:** `Any system. Same UMID. Latest version.`

---

### Scene 3: The Contract (10s)

**Visual:** A quick diagram showing the resolver's behavior:

- Request arrives: `GET myum.net/{UMID}`
- Resolver checks: Does the UMID exist? → Yes → Returns the manifest with a redirect to the canonical source.
- The consuming system validates: TTL check (fresh?), signature check (intact?), consent check (permitted?).

Three green checkmarks appear in sequence.

**Narration:** "The resolver is a thin lookup layer. It does not interpret the manifest — that is the consumer's job. It simply delivers the document. Trust is verified at the edges."

**On-screen text:** `universalmanifest.net`

---

## Production Notes

- **Key technical accuracy:** The resolver lives at `myum.net/{UMID}`, not at `universalmanifest.net` (which is the spec/docs site). Resolution returns the manifest via a `307` redirect to the canonical source. The consumer is responsible for validation — TTL freshness, signature integrity, and consent checking happen client-side. The resolver does not enforce trust policies; it is a lookup service.
- **Resolver contract:** The resolver responds with standard HTTP status codes: `307` for valid lookups, `404` for unknown UMIDs, `410` for revoked manifests. This contract is verified by the resolver test suite (WO-0116).
- **UM-pure framing:** The resolver is described as a specification-level concept, not a specific deployment. Any conformant resolver implementation can serve this role.
- **Visual palette:** Dark background (#0f172a). Vault: silver/steel with warm gold lighting when active. Request beam: bright blue. QR code: white on dark. Status indicators: green (#22c55e) for published/valid.
- **Sound design:** Vault closing: clean mechanical click. Request beam: swift "whoosh." Manifest appearing: bright reveal chime. Checkmarks: three ascending tones.
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
