# A Day with Universal Manifest

**Duration:** 2--3 minutes
**Format:** Narrative walkthrough / day-in-the-life animated explainer
**Audience:** Someone who understands the concept and wants to feel what it is like to actually live with UM. Potential adopters, community members, conference attendees.
**Tone:** Warm, personal, grounded. Less "feature demo," more "a day that just works." Think a Notion or Arc Browser lifestyle video -- human-centered, with technology receding into the background where it belongs.
**Character:** Sam -- a mixed-media artist who also builds tech tools. Creative, privacy-aware, pragmatic. They carry their manifest like they carry their phone: always with them, rarely thinking about it.

---

### Scene 1: Morning -- Update (30s)

**Visual:** Sam's apartment, morning light. Sam sits with coffee, opens a dashboard on their laptop. The screen shows their manifest in an organized, visual layout -- not raw JSON, but a friendly interface.

The manifest's structure is visible as sections:

- **Public profile** shard: display name ("Sam Torres"), bio, avatar thumbnail. A small edit icon beside it.
- **Portfolio** shard: a grid of artwork thumbnails. Sam drags a new piece -- a photograph titled "Neon Alley" -- into the grid. It slots in with a satisfying snap.
- **Consents panel:** A column of toggle switches. Sam scans them:
  - `publicDisplay: allowed` (green) -- unchanged.
  - `analytics.proofOfPlay: allowed` (green) -- unchanged.
  - Sam finds a new entry: "Sunset Gallery -- display permission." They flip it to **allowed** (green). The toggle clicks.
  - `ar.recording.faceVisible` is set to a custom value: "friends only" -- the toggle shows amber/yellow with a people icon.
  - `ar.recording.voiceAllowed: denied` (red) -- Sam checks it, nods, leaves it.
- **Devices** section: two enrolled devices listed. No changes needed.
- **TTL bar:** Along the bottom, the `issuedAt` and `expiresAt` timestamps are visible. As Sam saves their changes, the `issuedAt` updates to the current time. The `expiresAt` extends. The countdown bar refills.

Finally, a small cloud icon pulses -- the manifest syncs to the resolver at `myum.net`. The UMID is visible at the top: `urn:uuid:4a7c...` with a QR code.

**Narration:** "Morning. Sam opens their manifest dashboard. They add a new piece to their portfolio shard, grant display permission to a gallery they are visiting today, and double-check their smart-glasses consent -- face recording is set to friends only, voice recording is denied. They save. The manifest updates, the expiration refreshes, and the resolver syncs. Took about thirty seconds."

**On-screen text:** `Update. Consent. Sync.`

**Sound/Music:** Gentle morning acoustic-electronic blend. Soft interface sounds -- clicks, snaps, a gentle sync chime. Unhurried.

---

### Scene 2: Midday -- The Gallery (30s)

**Visual:** Sam arrives at Sunset Gallery -- a bright, modern art space. Jordan is inside, adjusting a display. As Sam walks through the door, a subtle visual effect: a thin beam of light travels from Sam's pocket (where the manifest icon glows faintly) to a small edge node mounted near the entrance.

Cut to: the gallery's system view. A terminal shows:

```
Fetching manifest: urn:uuid:4a7c...
Source: myum.net
```

The manifest arrives. The system opens it and runs through three checks, visualized as quick flashes:

1. **TTL check:** `expiresAt` is tomorrow. Green checkmark. `Fresh.`
2. **Consent check:** `publicDisplay: allowed`. Green checkmark. `Permitted.`
3. **Content policy match:** The gallery's venue manifest has `safeMode: PG-13`. Sam's portfolio shard lists `"contentRating": "PG-13"`. Green checkmark. `Compatible.`

Cut back to the gallery. Three large screens on the walls light up, each showing a different piece from Sam's portfolio shard -- including "Neon Alley," the piece they added this morning. Sam looks up, sees their work, and smiles. Jordan gives a thumbs-up from across the room.

Sam did not fill out a form. Sam did not email files. Sam did not sign a release. It just worked.

**Narration:** "Sam walks into Sunset Gallery for the first time. The gallery's system fetches Sam's manifest by UMID, checks that it is fresh, confirms display consent is allowed, and verifies the content rating matches the venue's policy. Within seconds, Sam's art appears on three screens. Sam did not lift a finger."

**On-screen text:** `Fetched. Validated. Displayed. Automatic.`

**Sound/Music:** A brighter beat kicks in as Sam enters the gallery. The three validation checks have quick ascending tones. Art appearing on screens is accompanied by a warm bloom sound and a subtle "wow" moment in the music.

---

### Scene 3: Afternoon -- The App (30s)

**Visual:** Sam sits in a cafe, phone in hand. They are trying a new social platform -- the sign-up screen is visible. Instead of the usual form (name, bio, profile picture, interests...), there is a single prominent button: "Connect with Universal Manifest." Below it, in small text: "Or fill out manually."

Sam taps the button. A prompt appears: "Share your UMID?" Sam confirms. The UMID is sent.

Cut to: the app's perspective. It fetches the manifest from the resolver. It opens the `publicProfile` shard and reads:

- `displayName: "Sam Torres"`
- `bio: "Mixed-media artist and toolmaker. Street photography, generative visuals, neighborhood rituals."`
- `avatarUrl: https://media.example.com/avatars/sam-torres.jpg`

These fields auto-fill into the profile form with a smooth cascade animation -- each field sliding into place.

But the app also checks what it cannot access. It looks for analytics consent: `analytics.tracking: not set` -- gray, denied by default. It looks for indexing consent: `search.indexing: not set` -- gray, denied by default. These fields are simply not requested. The app respects the boundaries.

Sam reviews the pre-filled profile. Everything looks right. They tap "Confirm." Done.

**Narration:** "At a cafe, Sam tries a new social platform. Instead of filling out another profile form, they share their UMID. The app fetches their manifest, reads the public profile shard, and pre-fills everything -- name, bio, avatar. The things Sam has not consented to -- analytics tracking, search indexing -- are not even requested. Sam reviews, confirms, and they are done."

**On-screen text:** `No forms. No re-entry. Boundaries respected.`

**Sound/Music:** Cafe ambient sounds underneath. The "Connect" button has a clean tap sound. Auto-fill cascade has a quick, satisfying ripple. A confident "done" tone when Sam confirms.

---

### Scene 4: Evening -- The Metaverse (30s)

**Visual:** Sam's living room, evening. They put on a VR headset. The scene transitions from the physical room to a virtual gallery opening -- a stylized, neon-lit digital space with other avatars milling around. Sam's avatar appears: it matches their manifest's cross-world profile -- display name "Sam Torres" floating above, a custom avatar loaded from the `metaverse.avatar` pointer, and friend connections visible in a subtle social overlay.

Sam mingles. An event organizer announces: "We will be recording tonight's event for a highlight reel."

Cut to: the recording system's view. It scans the room. For each avatar, it checks the person's manifest consent:

- **Avatar 1:** `metaverse.voiceCapture: allowed`. Green. Voice will be included.
- **Sam:** `metaverse.voiceCapture: allowed`. Green. `ar.recording.faceVisible: friends only` (amber). The system checks the relationship graph -- the recorder is not in Sam's friends list. Result: Sam's face is captured with a stylized mask overlay. Their voice is included.
- **Avatar 3:** `metaverse.voiceCapture: denied`. Red. Voice is filtered out of the recording.

The recording system processes these signals automatically. No one asks for permission forms. No one is interrupted. Consent is baked into the data layer.

**Narration:** "That evening, Sam enters a virtual gallery opening. Their avatar, display name, and social connections all carry over from their manifest. When someone records the event, Sam's consent settings are checked automatically. Voice recording: allowed. Face capture: friends only -- and the recorder is not a friend, so Sam's face gets a stylized mask. Another attendee denied voice capture entirely -- their voice is filtered out. Consent travels with the data."

**On-screen text:** `Your rules follow you -- even into virtual worlds.`

**Sound/Music:** The transition to VR is marked by a shift in the music -- more spacious, reverb-heavy, slightly futuristic. The consent checks are quick, subtle blips. The recording system's perspective is visualized with a camera-lens overlay.

---

### Scene 5: Night -- Review (20s)

**Visual:** Sam is back home, headset off, laptop open. The manifest dashboard shows a different view now: an activity summary for the day. This is not a log of manifest content -- it is an access log, referenced by UMID:

```
Today's activity:
- Sunset Gallery        read publicProfile, portfolio      2:14 PM
- Cafe Social App       read publicProfile                 3:47 PM
- VR Gallery Opening    read crossWorldProfile, consents   8:22 PM
- [auto-denied]         analytics.tracking                 3:47 PM  (Cafe Social App)
- [auto-denied]         ar.recording.faceVisible           8:31 PM  (VR Recording System)
```

Sam scans the list. Three systems accessed their profile today. One app read their public shard. Two consent requests were auto-denied because the permissions were not set or were explicitly restricted.

Sam notices that Sunset Gallery is on the list -- they visited today, and it worked great. They think about tomorrow: they are visiting a different gallery. They open the consents panel and add a new entry: "Night Owl Gallery -- display permission: allowed." The toggle clicks green.

The manifest updates. The `issuedAt` refreshes. The resolver syncs. The countdown bar refills.

Sam closes the laptop.

**Narration:** "Before bed, Sam checks their manifest's activity log. Three venues accessed their profile today. One app read their public shard. Two consent requests were auto-denied -- one for analytics tracking, one for face recording by someone outside their friend list. Sam adjusts a consent for tomorrow's gallery visit, and the manifest updates instantly across all systems."

**On-screen text:** `See who accessed what. Adjust anytime.`

**Sound/Music:** Music has settled into a calm, reflective mode. Soft ambient tones. The sync chime is gentle -- a day's-end sound.

---

### Scene 6: Close (10s)

**Visual:** Sam's laptop screen fades. The manifest card rises from it and floats to the center of the screen, glowing warmly. The day's five scenes replay as tiny vignettes orbiting the card -- morning dashboard, gallery screens, cafe app, VR world, nighttime review. They fade into the card.

The Universal Manifest wordmark appears below. The tagline appears. The URL fades in.

**Narration:** "Sam's data. Sam's rules. One manifest, everywhere."

**On-screen text:** `Sam's data. Sam's rules. One manifest, everywhere.` | `universalmanifest.net`

**Sound/Music:** A final, warm resolving chord. The music fades gently. Silence.

---

## Production Notes

### Pacing and structure
- This is the longest script in the series. It should feel like a story, not a feature list. The audience should empathize with Sam's day and think, "I want my data to work like that."
- Each scene is a self-contained mini-narrative but builds on the previous one. Morning sets up the manifest. Midday shows it in action passively. Afternoon shows active sharing. Evening shows consent complexity. Night provides closure and control.

### Character details
- Sam is both an artist and a technologist -- they understand the system but interact with it casually, like checking the weather. The manifest is not the center of Sam's day; it is infrastructure that recedes into the background.
- Jordan appears briefly in Scene 2 (background, gallery operator).
- Anonymous characters populate Scenes 4 (VR attendees) and 3 (cafe background).

### Technical accuracy
- **Scene 1 (Morning):** The manifest structure shown matches the real spec: `shards` array with named shards, `consents` array with `@type: "um:Consent"`, `issuedAt`/`expiresAt` timestamps, UMID as `@id`, resolver sync to `myum.net`.
- **Scene 2 (Gallery):** The gallery's system fetches by UMID, validates TTL (expiresAt), checks consent (`publicDisplay: allowed`), and matches content policy (`safeMode: PG-13`). This matches the venue-edge-manifest and creator-public-capsule-manifest fixtures.
- **Scene 3 (App):** The app reads the `publicProfile` shard (name, bio, avatar). Absent consents are denied by default -- this is the consent-default-deny pattern proven in Journey 10.
- **Scene 4 (Metaverse):** Avatar and social data come from pointers (`metaverse.avatar`, `metaverse.socialGraph`). Voice capture consent (`metaverse.voiceCapture`) and face visibility are from the metaverse and smart-glasses fixtures. The "friends only" granularity is modeled as a consent value -- real fixtures use `"allowed"`, `"denied"`, and `"restricted"`.
- **Scene 5 (Night):** The activity log references manifests by UMID, not by content. Auto-denied entries reflect the consent-default-deny behavior. The resolver syncs when the manifest is updated.

### Visual consistency
- Same color palette, typography, and character style as the other scripts in this series.
- The manifest dashboard in Scenes 1 and 5 should look like a real product interface -- clean, organized, not abstract. Think of it as a preview of what a UM management tool could look like.
- The VR world in Scene 4 should be stylized but not cartoonish -- it is a plausible near-future metaverse environment.

### Aspect ratios to deliver
- 16:9 (primary)
- 1:1 (social clips -- each scene could be extracted as a standalone clip)
- 9:16 (stories/reels -- Scene 2 "The Gallery" and Scene 3 "The App" work particularly well as vertical shorts)
