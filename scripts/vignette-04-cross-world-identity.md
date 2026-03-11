# V-04: Cross-World Identity

**Duration:** 30–45 seconds
**Format:** Motion graphics / animated explainer
**Audience:** Metaverse-curious audiences, game developers, XR platform architects, standards body members.
**Tone:** Energetic, visual, slightly cinematic.
**Concept:** A single Universal Manifest carries identity across completely different platforms, renderers, and virtual worlds. No re-registration, no data loss, no lock-in.

---

### Scene 1: The Portal Jump (12s)

**Visual:** A stylized character — "Nova" — stands in a neon-lit virtual world (World A). The environment has a distinct art style: angular, cyberpunk-inspired. Nova's display name floats above their head. Their avatar is fully loaded — a distinctive 3D model.

A portal appears — a glowing doorway. Nova leaps through it.

Nova lands in a completely different world (World B) — organic, fantasy-themed, different lighting, different physics. But Nova still looks like Nova. Same avatar. Same display name. Their friend list appears in the HUD. The transition is seamless.

**Narration:** "Nova jumps from one virtual world to another — completely different platform, completely different renderer. But their avatar, display name, and social connections carry over instantly. No re-registration. No data loss."

**On-screen text:** `Same identity. Different worlds.`

---

### Scene 2: How It Works (15s)

**Visual:** A quick cutaway showing the mechanics. Nova's Universal Manifest card appears between the two worlds. The manifest opens to reveal:

- A `crossWorldProfile` Facet (blue) containing `displayName: "Nova"` and `supportedWorlds: ["rp1://...", "portal://..."]`.
- A `metaverse.avatar` pointer (coral arrow) reaching outward to a 3D model asset hosted externally.
- A `metaverse.socialGraph` pointer (coral arrow) reaching to a friend-list service.
- A `metaverse.profilePublic` consent toggle — set to green (allowed).

World B's system reads the manifest. It follows the avatar pointer to fetch Nova's 3D model. It follows the social graph pointer to load the friend list. It checks the consent toggle — profile is public. Everything loads.

**Narration:** "The secret is the manifest. World B reads Nova's cross-world profile Facet, follows the avatar pointer to fetch the 3D model, loads the social graph, and checks consent — all from one portable document. The manifest is the bridge."

**On-screen text:** `One manifest bridges every world`

---

### Scene 3: Close (8s)

**Visual:** Nova stands confidently between the two worlds, the manifest glowing in the space between them. More portals open in the background — three, four, five different worlds, all connected through the same manifest.

**Narration:** "One identity. Every world. No walls."

**On-screen text:** `universalmanifest.net`

---

## Production Notes

- **Key technical accuracy:** The `crossWorldProfile` Facet carries identity metadata that is renderer-agnostic. Avatar assets are external — loaded via `metaverse.avatar` pointer URLs, not embedded in the manifest. The `supportedWorlds` field declares which platforms/renderers the identity is compatible with. Consent for profile visibility is checked via the `metaverse.profilePublic` consent toggle.
- **UM-pure framing:** This vignette describes the portaling concept in terms of the UM specification only. The two "worlds" are generic platforms — no PeerMesh branding, no specific product references. The portal is a conceptual doorway, not a specific product feature.
- **Hackathon validation:** This exact pattern was proven in the peer-mesh-spatial-fabric hackathon, where the Portal server on port 3333 resolved Universal Manifests and loaded avatar assets from pointer URLs into a Three.js renderer. The dual-format normalization (UM v0.1 + Manifest Commons) demonstrated that different systems can consume the same manifest.
- **Visual palette:** Dark background (#0f172a). World A: neon blue/purple tones. World B: warm amber/green tones. Manifest glow: warm gold. Portal: bright white with iridescent edges.
- **Sound design:** Portal jump has a dramatic "whoosh" transition. Avatar loading in World B has a satisfying "materialization" shimmer. Close has a confident resolving chord.
- **Aspect ratios:** 16:9 (primary), 1:1 (social), 9:16 (stories/reels).
