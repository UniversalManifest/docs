# How Universal Manifest Works

**Duration:** 90--120 seconds
**Format:** Conceptual technical walkthrough / animated explainer
**Audience:** Non-technical but curious. They know what UM is and want to understand the mechanics.
**Tone:** Friendly, modern, slightly playful but credible. Think Stripe or Linear documentation videos.

---

### Scene 1: Meet the Manifest (15s)

**Visual:** A blank canvas. A document outline materializes -- a glowing card shape. Fields appear one by one, sliding into place like puzzle pieces. First, the `@id` field lights up at the top as a serial number with a small QR code beside it -- the UMID. Then `subject` appears, showing a DID string (e.g., `did:key:z6Mki...`) with a small person silhouette. Then `issuedAt` and `expiresAt` slide in along the bottom edge as a horizontal timeline bar with a countdown clock. The card pulses once -- it is alive.

**Narration:** "Every Universal Manifest starts with the same structure. A unique identifier -- the UMID -- so any system can look it up. A subject -- who or what the manifest is about. And a time window: when it was issued and when it expires. Think of it as a smart passport for your data."

**On-screen text:** `UMID: unique lookup key` | `Subject: who it's about` | `TTL: when it expires`

**Sound/Music:** Clean electronic track begins, steady and confident. Soft chime as each field appears. A subtle heartbeat pulse when the card activates.

---

### Scene 2: Shards -- The Tools (20s)

**Visual:** The manifest card transforms into the Swiss Army Knife. It rotates slowly. Then, one by one, tools fold out from the body:

- **Tool 1:** A profile picture frame folds out -- labeled `publicProfile`. Inside: a display name, bio text, and avatar image thumbnail. A small person icon glows beside it.
- **Tool 2:** A key card folds out -- labeled `deviceRegistration`. Inside: a device name, model number, and capability list. A small screen icon glows beside it.
- **Tool 3:** A badge folds out -- labeled `claims`. Inside: role badges (creator, venue, display) and verification stamps. A small shield icon glows beside it.
- **Tool 4:** An arrow folds out -- labeled `pointers`. Unlike the others, this one does not contain data -- it is a beam of light pointing outward to external URLs. A small link icon glows beside it.

Each tool is a different accent color. After all four are deployed, the knife holds steady, showing the full complement.

**Narration:** "Inside the manifest, data is organized into shards -- named sections, each carrying different information for different situations. A public profile shard for social apps. A device registration shard for hardware. A claims section for credentials and roles. And pointers -- these do not copy data into the manifest. Instead, they reference where the authoritative data lives, so consumers always get the freshest version."

**On-screen text:** `Shards: named data sections` | `Pointers: references, not copies`

**Sound/Music:** Satisfying metallic click for each tool deployment. A brief melodic progression as each tool appears -- building complexity.

---

### Scene 3: Consent -- The Locks (20s)

**Visual:** Riley appears -- privacy-conscious, thoughtful. They hold their own manifest (Swiss Army Knife form). The camera zooms into the consent compartment, which opens to reveal a panel of toggle switches, each with a label:

- `ar.recording.faceVisible` -- Riley flips it. It clicks to **denied** (red, padlock snaps shut).
- `social.profilePublic` -- Riley flips it. It clicks to **allowed** (green, padlock opens).
- `analytics.proofOfPlay` -- Riley considers, then leaves it unset. The switch stays gray. A small label appears: "Not set = denied by default." The padlock stays shut.

Now a system (represented by a probe beam from an app icon) tries to access Riley's profile: the beam passes through the green toggle. It tries to access face recording: the beam hits the red lock and deflects with a spark. It tries analytics: the beam hits the gray lock -- same result, deflected.

Riley nods, satisfied.

**Narration:** "Consent is built in, not bolted on. Every manifest can carry consent toggles -- explicit yes-or-no signals for specific uses. Want your profile on social media? Flip it to allowed. Want smart glasses to record your face? Denied. And here is the key: if a consent is not set at all, it defaults to denied. Nothing gets through unless you open the lock."

**On-screen text:** `Green = allowed` | `Red = denied` | `Gray (not set) = denied by default`

**Sound/Music:** Satisfying click-lock sounds for each toggle. A warm "access granted" chime when the beam passes through green. A firm "blocked" sound when beams deflect off red and gray.

---

### Scene 4: Publishing and Resolving (20s)

**Visual:** Alex appears with their manifest. They walk toward a large, elegant vault -- the resolver, labeled `myum.net`. Alex places the manifest into an open slot. The vault door closes with a secure click. The UMID serial number illuminates on the outside of the vault -- it is now registered.

Cut to: Jordan, at their gallery, at a different location. Jordan opens a terminal or search interface. They type the UMID (`urn:uuid:9b1d...`). The request travels as a beam of light across the screen to the vault. The vault opens, and a fresh copy of the manifest appears on Jordan's screen. The TTL bar at the bottom is full -- this is the latest version.

A small clock icon appears: "Last updated 5 minutes ago." Alex, meanwhile, has updated their manifest at their own location -- the vault receives the update, and the next time Jordan checks, the new version appears.

**Narration:** "Once Alex publishes their manifest to the resolver -- a lookup service at myum.net -- anyone with the UMID can fetch it. Jordan, a venue operator in another city, types in the UMID and gets Alex's manifest. Always the latest version. Published once, available everywhere, always up to date."

**On-screen text:** `Publish to resolver` | `Fetch by UMID` | `Always current`

**Sound/Music:** Vault closing: heavy but clean mechanical sound. Request beam: a swift "whoosh." Manifest appearing: a bright reveal chime.

---

### Scene 5: Validation (15s)

**Visual:** Jordan's system receives Alex's manifest. It enters a checkpoint -- a scanning station with three sequential gates:

- **Gate 1 -- Freshness:** A clock icon checks the `expiresAt` timestamp against the current time. The countdown bar is still green. A checkmark appears. `TTL valid.`
- **Gate 2 -- Integrity:** A fingerprint scanner reads the `signature` block. The Ed25519 algorithm label glows. The canonical payload is compared to the signature value. A checkmark appears. `Signature valid.`
- **Gate 3 -- Consent:** The scanner reads the consent toggles. It checks whether the venue has permission for `publicDisplay`. The toggle is green. A checkmark appears. `Consent granted.`

All three gates show green checkmarks. The manifest passes through and arrives, intact, on Jordan's display system.

**Narration:** "Before a system uses a manifest, it validates. Is it expired? Check the timestamps. Is the data tampered with? Verify the cryptographic signature. Does the user allow this use? Check the consent toggles. All green? The manifest is trusted."

**On-screen text:** `1. Freshness (TTL)` | `2. Integrity (signature)` | `3. Permission (consent)`

**Sound/Music:** Three ascending tones for each gate passing. A final "approved" sound -- confident and clean.

---

### Scene 6: The Result (15s)

**Visual:** A rapid montage of the manifest working across contexts, each scene lasting 3--4 seconds:

- **Gallery:** Alex's art appears on screens at Jordan's venue. The publicProfile shard and public capsule data are being read. The manifest glows softly in the corner of the display.
- **Social app:** Sam, a developer, builds an app that reads the publicProfile shard to auto-fill a user's profile page. No duplicate forms.
- **Smart glasses:** A person wearing smart glasses walks past Riley. The glasses check Riley's manifest -- `ar.recording.faceVisible: denied`. Riley's face is automatically blurred in the glasses' view.
- **Virtual world:** A game character leaps between two virtual worlds. Their avatar, display name, and social connections carry over through the crossWorldProfile shard and metaverse pointers.

All four scenes merge into a single flowing visual -- the manifest at the center, with light beams connecting to each context.

**Narration:** "One format. Built once. Works everywhere. From galleries to apps, from smart glasses to virtual worlds -- the same manifest, the same consent controls, the same trust."

**On-screen text:** `One format. Built once. Works everywhere.`

**Sound/Music:** Music reaches its peak -- all melodic layers together. Resolves cleanly.

---

## Production Notes

- **Pacing:** This video is denser than "What Is UM?" -- it teaches mechanics. Each scene should breathe but not linger. Use visual transitions (the manifest transforming, traveling, being scanned) to maintain flow.
- **Character use:** Alex appears in scenes 1, 4, and 6. Riley owns scene 3. Jordan appears in scenes 4, 5, and 6. Sam appears briefly in scene 6. The manifest itself is a constant presence throughout.
- **Technical accuracy:**
  - Shards are arrays of objects with `@type: "um:Shard"` and a `name` field.
  - Consents are arrays of objects with `@type: "um:Consent"`, `name`, and `value` (`"allowed"` or `"denied"`).
  - Pointers contain `name` and `url` -- they are references, not embedded data.
  - The signature uses Ed25519 + JCS canonicalization (v0.2 profile).
  - The resolver lives at `myum.net/{UMID}`, not the spec site.
  - TTL is defined by `issuedAt` and `expiresAt` timestamps, not a duration field.
- **Color palette:** Same as "What Is UM?" script for brand consistency.
- **Aspect ratios to deliver:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
