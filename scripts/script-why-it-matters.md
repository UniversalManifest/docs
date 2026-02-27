# Why Universal Manifest Matters

**Duration:** 60--90 seconds
**Format:** Impact montage / vignette-driven explainer
**Audience:** Someone who understands what UM is and wants to see why it is valuable. Decision-makers, potential adopters, curious technologists.
**Tone:** Confident, visual, slightly cinematic. Each vignette is a micro-story. Think Apple product videos crossed with Notion use-case reels.

---

### Scene 1: Intro (5s)

**Visual:** A single glowing manifest card rotates slowly in the center of a dark canvas. Five faint icons orbit it -- a gallery frame, smart glasses, a game controller, a fingerprint, and a display screen. They pulse gently, waiting.

**Narration:** "Universal Manifest is already changing how systems share data. Here is what that looks like."

**On-screen text:** `Five stories. One manifest.`

**Sound/Music:** A clean, confident electronic track begins -- minimal, building. A low tone that promises momentum.

---

### Scene 2: Vignette 1 -- The Gallery (12s)

**Visual:** Alex walks into a gallery they have never visited before -- Sunset Gallery, Jordan's venue. As Alex crosses the threshold, a subtle light pulse travels from Alex's pocket (where their manifest glows) to the gallery's system (a small edge node on the wall). The system fetches Alex's manifest by UMID. It opens the `publicCapsule` shard: display name, bio, featured artworks. It checks the `publicDisplay` consent toggle -- green, allowed. It checks the `safeMode` claim against the venue's content policy -- PG-13, match.

Within seconds, three screens in the gallery light up with Alex's art. Alex looks up, surprised and delighted. They did not lift a finger.

**Narration:** "Alex walks into a gallery they have never visited. Their art appears on the screens within seconds. The venue read their manifest, found their public capsule, checked their consent, confirmed the content rating matched -- all automatically."

**On-screen text:** `Consent-checked. Policy-matched. Instant.`

**Sound/Music:** A warm, rising tone as Alex enters. Soft "connection established" chime. The art appearing on screens is accompanied by a gentle visual bloom.

---

### Scene 3: Vignette 2 -- The Smart Glasses (12s)

**Visual:** A busy sidewalk. Someone wearing sleek AR smart glasses walks past Riley. The glasses' field of view is shown as a translucent overlay. As Riley enters the frame, the glasses' system sends a quick lookup -- a beam reaches out toward Riley's manifest UMID (broadcast via a proximity protocol or looked up through the resolver). The manifest arrives. The glasses check `ar.recording.faceVisible` -- **denied** (red). `ar.recording.voiceAllowed` -- **denied** (red).

Immediately, Riley's face in the glasses' view is replaced with a smooth, respectful blur. Their voice, if captured in ambient audio, is filtered out. A small shield icon appears beside Riley's silhouette in the AR overlay. Riley walks on, unbothered and unrecorded.

**Narration:** "Someone wearing smart glasses walks past Riley. The glasses check Riley's manifest. Recording consent: denied. Automatically, Riley's face is blurred and their voice is filtered. Privacy, enforced by default."

**On-screen text:** `Consent: denied. Privacy: enforced.`

**Sound/Music:** A brief tension note as the glasses scan. A firm but not aggressive "blocked" sound when consent is denied. A calm resolution as Riley walks on.

---

### Scene 4: Vignette 3 -- The Virtual World (12s)

**Visual:** A stylized game character -- "Nova" -- stands in a neon-lit virtual world (World A). A portal appears. Nova leaps through it and lands in a completely different world (World B) -- different art style, different lighting, different environment. But Nova still looks like Nova. Their avatar is intact. Their display name floats above their head. Their social connections (friend list) are visible in the HUD.

How? A quick cutaway shows the manifest's `crossWorldProfile` shard being read by World B's system. The `metaverse.avatar` pointer is fetched -- it resolves to Nova's avatar asset. The `metaverse.socialGraph` pointer is fetched -- friend list loads. The `metaverse.profilePublic` consent is checked -- allowed. Everything carries over.

**Narration:** "Nova jumps from one virtual world to another. Their avatar, display name, and social connections carry over seamlessly. Same manifest, different worlds. No re-registration, no data loss."

**On-screen text:** `Same identity. Different worlds. Zero friction.`

**Sound/Music:** A playful, energetic beat for the portal jump. A satisfying "connection complete" sound as the data loads in World B.

---

### Scene 5: Vignette 4 -- The Proof (12s)

**Visual:** Sam, a developer, has built a new platform. A new user arrives at the sign-up screen. Instead of a CAPTCHA or an ID upload, the user shares their UMID. Sam's app fetches the manifest from the resolver. It opens the `claims` section. Inside: two proof-of-personhood verification claims from different providers -- `personhood.worldId.verification: verified` (issued by `did:web:worldcoin.org`) and `personhood.brightId.verification: verified` (issued by `did:web:brightid.org`). Each claim has a pointer to the verification endpoint.

Sam's app checks both. Two green checkmarks appear. The user is verified as a unique human -- in seconds, with no personal data exposed. No name, no photo, no address was needed. Just the proof.

**Narration:** "Sam's app needs to verify a user is a real person, not a bot. The user's manifest contains proof-of-personhood credentials from two different providers. Verified in seconds. No personal data exposed."

**On-screen text:** `Proof without exposure. Verified in seconds.`

**Sound/Music:** A clean, precise rhythm. Two ascending tones for the two verification checks. A confident "verified" chime.

---

### Scene 6: Vignette 5 -- The New Device (12s)

**Visual:** A new display screen -- a large mounted TV -- is plugged in at a venue. It powers on with a blank screen. A small edge node nearby detects it. The edge node holds the venue's manifest. The venue manifest contains a `devices` section with enrolled devices and a `venuePolicy` shard with content rules (PG-13, no nudity, preferred tags: local art, photography).

The new screen sends a registration request. The venue manifest's `deviceRegistration` shard is read. The device is enrolled -- its DID appears in the `devices` array. The content policy downloads. The screen starts showing curated art -- thumbnails slide into place, all matching the venue's content rules. Zero manual configuration. No one touched a keyboard.

**Narration:** "A new display is plugged in at a venue. It reads the venue's manifest, enrolls itself, downloads the content policy, and starts showing curated art. Zero manual configuration."

**On-screen text:** `Plug in. Enroll. Display. Automatic.`

**Sound/Music:** A mechanical "power on" sound. A quick "enrolled" chime. Art appearing on screen accompanied by a warm visual bloom.

---

### Scene 7: Close (10s)

**Visual:** The five vignette scenes shrink into small panels that orbit the central manifest card -- the same visual from the intro, but now all five icons are fully lit and active. The panels merge into the manifest, which pulses brightly and then settles. The Universal Manifest wordmark appears below. The tagline appears. The URL fades in.

**Narration:** "One document. Every system. Your rules."

**On-screen text:** `One document. Every system. Your rules.` | `universalmanifest.net`

**Sound/Music:** All musical layers converge. A final, resolving chord. Subtle shimmer on the URL.

---

## Production Notes

- **Pacing:** Each vignette is a self-contained micro-story. They should feel like quick, punchy reveals -- not lingering dramas. The energy builds across the five vignettes.
- **Character assignments:**
  - Vignette 1: Alex (creator) + Jordan (venue operator, background)
  - Vignette 2: Riley (privacy guardian) + anonymous glasses wearer
  - Vignette 3: "Nova" (metaverse character, avatar of the manifest user)
  - Vignette 4: Sam (app developer) + anonymous new user
  - Vignette 5: No human character -- the device and the venue manifest are the actors
- **Technical accuracy across vignettes:**
  - Vignette 1 references real fixture structure: `publicCapsule` shard, `publicDisplay` consent, `safeMode` claim.
  - Vignette 2 references real fixture structure: `ar.recording.faceVisible` and `ar.recording.voiceAllowed` consents from the smart-glasses-consent-denied fixture.
  - Vignette 3 references real fixture structure: `crossWorldProfile` shard, metaverse pointers (`metaverse.avatar`, `metaverse.socialGraph`), `metaverse.profilePublic` consent.
  - Vignette 4 references real fixture structure: `personhood.worldId.verification` and `personhood.brightId.verification` claims with issuer DIDs.
  - Vignette 5 references real fixture structure: venue manifest's `devices` array, `venuePolicy` shard with `safeMode` and `contentRules`, device enrollment via DID.
- **Visual consistency:** Same color palette, typography, and character style as the other scripts in this series.
- **Aspect ratios to deliver:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
