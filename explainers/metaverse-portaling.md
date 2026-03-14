# Metaverse Universal Manifest (MUM) Explainer: Portaling

## Video 1: "Jumping Worlds with Your Stuff" (The MUM Concept)

**Target Audience:** Creators, players, and developers interested in interoperable virtual worlds.
**Goal:** Explain the Metaverse Universal Manifest (MUM) as the specific portable envelope that lets a person jump between different platforms while carrying onboarding projection, consent propagation, compliance proofs, social reputation, and preference bundles.

---

### Scene 1: The Problem (0:00 - 0:30)
- **Visuals:** An animated character named "Nova" stands in "Neon City" (Platform A). She has a cool custom jacket, a glowing sword, and a friends list.
- **Action:** Nova walks through a portal to "Fantasy Realm" (Platform B).
- **The Result:** The moment she arrives, she loses everything. She's downgraded to a default grey avatar. Her jacket is gone. Her sword is gone. Her friends list is empty.
- **Narrative (Voiceover):** "We've all been there. You build your identity, collect your gear, and make friends in one virtual world... but the moment you jump to another platform, you start completely from scratch. The metaverse is broken into silos. You can't take *you* with you."

### Scene 2: The Solution - Metaverse Universal Manifest (MUM) (0:30 - 1:15)
- **Visuals:** Rewind time. Nova is back in Neon City. A glowing, floating "Capsule" (or envelope) appears next to her: The Metaverse Universal Manifest, or MUM.
- **Action:** We peek inside the capsule. It contains simple, readable building blocks covering the five core MUM scenarios:
  - **Identity & Asset Projection:** Nova's global ID and Avatar/Inventory pointers.
  - **Consent Propagation:** Clear privacy rules (e.g., "Allow public profile", "Deny voice capture").
  - **Compliance Transactions:** Proof that she meets age or entry requirements.
  - **Social & Reputation Portability:** Links to her friends list and gathered trust scores.
  - **Preferences Bundle:** Her saved interface settings and accessibility needs.

### Scene 3: The Portaling Experience (1:15 - 2:00)
- **Visuals:** Nova steps into the portal to "Fantasy Realm" again, but this time, her MUM capsule travels with her.
- **Action:** As she arrives, Fantasy Realm instantly "reads" the envelope across all MUM parameters:
  1. **Onboarding Projection**: It loads her custom character model and restores compatible inventory.
  2. **Consent Propagation**: The platform asks to turn on her mic, but MUM says `voiceCapture = denied`, so it automatically mutes her.
  3. **Social Portability**: Her friends list populates with familiar faces already in this realm.
  4. **Compliance Checking**: It verifies her age gate requirements silently through the manifest.
  5. If one cosmetic item is unsupported, the platform falls back gracefully instead of failing the whole jump.


### Scene 3b: The Seamless Transition — Loading Content (2:00 - 2:20)
- **Visuals:** Rewind slightly. Nova steps into the portal again. Instead of a black screen or a loading bar, the portal itself transforms — Fantasy Realm's branded loading screen appears around her. She sees Fantasy Realm's logo, a stylized landscape preview, and a message: "Preparing your arrival..."
- **Action:** While Nova watches the loading experience, a translucent sidebar shows the technical steps happening behind the scenes: manifest transfer, consent verification, avatar pointer resolution, signature checking. Each step completes with a quiet checkmark. When the last step finishes, the loading screen dissolves seamlessly into the live Fantasy Realm world — Nova is already there.
- **Narrative (Voiceover):** "But what about the gap between leaving Neon City and arriving in Fantasy Realm? With loading content pointers in the manifest, the destination world sends its branded loading experience to the source world *before* the full handshake completes. Nova never sees a blank screen. She's visually immersed in Fantasy Realm's world from the moment she steps into the portal — even while consent checks, avatar loading, and signature verification happen behind the scenes. It's the same pattern AAA games use: show the next level's content while it loads."

### Scene 4: How It Works Under the Hood (2:20 - 2:50)
- **Visuals:** Split screen. On the left, Nova enjoying the world. On the right, a simplified, color-coded glimpse of the JSON-LD code, highlighting a `crossWorldProfile` facet. We show a cryptographically secure signature locking the code, plus freshness TTL timers.
- **Action:** An animated lock snaps shut on the document. A stamp says "Verified by Cryptography. No Central Authority Required. Cache Freshness Enforced."


### Scene 5: The Future of Portability (2:30 - 3:00)
- **Visuals:** Montage of different scenarios. The same glowing MUM envelope being scanned at a virtual concert, maintaining social reputation in a competitive game, and proving compliance at a virtual storefront.
- **Action:** The text "Build Your Metaverse Universal Manifest Today" appears on screen with a link to `universalmanifest.net`.


---

### Key Takeaways for the Animator/Editor:
- Emphasize the **Capsule/Envelope** metaphor. UM should feel like a protective, portable carrier.
- Keep the technical JSON aspects very lightweight—show it as colorful, readable building blocks (Identity, Consents, Pointers) before flashing the code.
- Highlight **Consents**: portaling is not just about dragging items along; it is about carrying *privacy boundaries* along too.
- Show **graceful degradation**: unsupported items should fall back cleanly, not break the whole jump.
