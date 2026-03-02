# Universal Manifest -- Animation Production Briefing

A handoff document for animation producers, motion designers, and AI animation tools. This document describes the visual language, characters, metaphors, and creative direction for producing explainer animations about Universal Manifest.

---

## Core Metaphor: "The Swiss Army Knife of Personal Data"

Universal Manifest is a portable document that carries identity, credentials, preferences, and permissions between systems. The central visual metaphor is a **Swiss Army Knife** -- a single compact object with fold-out sections, each serving a different purpose, with built-in locks that control which sections can be opened.

### How to Visualize the Manifest

The manifest should be represented as a **glowing, compact card or document** -- roughly credit-card sized, with a subtle luminous border. It feels solid and trustworthy, not flimsy. Think of it as halfway between a passport and a high-tech keycard.

Key visual properties:

- **Shape:** Rounded rectangle, slightly thicker than a credit card, with visible depth suggesting internal structure
- **Surface:** Matte dark material (matching the project's dark-mode palette) with a glowing seal/emblem on the front
- **Glow:** Soft bright-blue edge glow that intensifies when the manifest is active (being read, validated, or transmitted)
- **Seal:** A small circular emblem on the front face -- the UM logo or a stylized lock icon
- **Serial number:** The UMID is faintly engraved along the bottom edge, visible on close-up

When the manifest "opens," its sections should fold out like the tools of a Swiss Army Knife -- panels hinging outward from the main body, each with its own icon and color accent.

---

## Visual Vocabulary

Each core concept in Universal Manifest has a specific visual representation. Use these consistently across all animations.

### Manifest

- **Visual:** Glowing card/document with a seal on the front face
- **Animation:** Floats slightly above surfaces, rotates gently when idle, glows brighter when active
- **Sound:** Soft, clean chime when it appears or is activated

### Shards

- **Visual:** Fold-out panels that hinge from the manifest's edges, like compartments in a Swiss Army Knife. Each panel has a distinct icon representing its data type.
- **Icons by shard type:**
  - Public Profile: silhouette/avatar icon
  - Device Registration: device/screen icon
  - Venue Policy: building/shield icon
  - Game Profile: controller/trophy icon
  - Credentials: badge/certificate icon
- **Animation:** Panels fold out smoothly with a satisfying mechanical motion. When a shard is being read, its panel glows and a data stream flows from it to the consuming system.
- **Color:** Panels use the bright-blue accent color by default, with the icon in white

### Pointers

- **Visual:** Thin, luminous arrows or tether lines that extend from the manifest outward to other systems. The arrow tip touches the target system; the base connects to the manifest.
- **Animation:** Arrows draw themselves from the manifest to the target, pulsing gently to indicate a live reference. When data is fetched, a brief data-packet animation travels along the arrow.
- **Color:** Bright blue, slightly more transparent than the manifest glow

### Consent

- **Visual:** Small toggle locks on each shard panel. Green (unlocked, glowing) = allowed. Red (locked, matte) = denied.
- **Animation:** Toggles flip with a clean click. When a system tries to access a denied shard, the red lock briefly flashes and the panel stays closed. When access is allowed, the green lock glows and the panel opens smoothly.
- **Sound:** Click for toggle. Soft denial tone (low) for red. Soft approval tone (high) for green.

### TTL (Time-to-Live / Validity Window)

- **Visual:** A small countdown timer or hourglass embedded in the manifest's top-right corner. The sand/progress drains over time.
- **Animation:** Timer visibly counts down. When the manifest expires, the glow fades, the timer runs out, and the manifest becomes translucent and gray (visually "dead"). Optionally, a brief dissolve animation.
- **Color:** Timer starts bright blue, transitions to amber in the last 20%, then red at expiry.

### UMID (Universal Manifest Identifier)

- **Visual:** A unique serial number engraved along the bottom edge of the manifest card. On close-up, it's a formatted string (e.g., `urn:uuid:2b5f...`).
- **Animation:** When a resolver lookup happens, the UMID glows and a search beam extends from it to the resolver service.

### Resolver (myum.net)

- **Visual:** A secure locker room or filing cabinet. Rows of glowing slots, each containing a manifest card. When a UMID is queried, the correct slot lights up and the manifest slides out.
- **Animation:** Camera approaches the locker room, a search query travels in, the matching slot illuminates, and the manifest emerges and floats to the requester.
- **Color:** Deep blue-gray interior with bright-blue slot accents

### Validation

- **Visual:** A scanner or checkpoint gate. The manifest passes through; a scanning beam sweeps across it. A green checkmark or red X appears on the other side.
- **Animation:** Manifest approaches the gate, pauses as the scan beam crosses it left-to-right, then either (a) green flash + checkmark + manifest passes through glowing, or (b) red flash + X + manifest is pushed back.
- **Sound:** Scanning hum during the sweep. Approval chime or denial tone at the result.

---

## Recurring Characters

These characters appear across all animation scripts. They represent different perspectives on Universal Manifest.

### Alex (The Creator)

- **Role:** A freelance digital artist who carries a manifest everywhere
- **Visual:** Young adult, creative casual clothing, carries a tablet or sketchpad. Their manifest is always visible -- floating near their shoulder or tucked into a pocket that glows faintly.
- **Personality:** Enthusiastic, slightly disorganized, values freedom and portability. They're the "carry my world with me" archetype.
- **Use case focus:** Portable profiles, venue check-ins, public display permissions

### Jordan (The Venue Operator)

- **Role:** Runs an art gallery/venue, needs to trust incoming manifests
- **Visual:** Professional but approachable, standing at a gallery entrance or behind a control panel. Their environment has validation scanners and display screens.
- **Personality:** Practical, security-conscious, wants things to "just work." They're the "I need to trust what I receive" archetype.
- **Use case focus:** Manifest validation, consent checking, display rendering, offline operation

### Sam (The App Developer)

- **Role:** Building a social platform, wants portable user profiles
- **Visual:** Developer aesthetic -- hoodie, laptop, coffee. Surrounded by floating code snippets and API endpoints. Often shown at a desk with multiple screens.
- **Personality:** Curious, efficiency-driven, hates building custom integrations. They're the "just give me one format" archetype.
- **Use case focus:** Parsing manifests, consuming shards, progressive adoption, reference implementation usage

### Riley (The Privacy Guardian)

- **Role:** A privacy-conscious user who controls everything
- **Visual:** Composed, deliberate. Their manifest has many visible locks (consent toggles), most of them red/locked. They interact with their manifest carefully, opening and closing permissions.
- **Personality:** Thoughtful, protective, values control. They're the "nothing without my permission" archetype.
- **Use case focus:** Consent management, default-deny model, expiry controls, selective sharing

### The Manifest (Animated Object)

- **Role:** The Swiss Army Knife itself, personified
- **Visual:** The glowing card described above, but with subtle personality cues -- it tilts to "look" at things, glows warmer when it's being used helpfully, dims when it's being misused or has expired.
- **Personality:** Reliable, compact, quietly capable. It doesn't draw attention to itself until it's needed, then it opens exactly the right tools. Think of it as a loyal, competent assistant.
- **Animation style:** Smooth, mechanical movements for fold-outs. Organic, warm glow changes for emotional beats.

---

## Color Palette

Reference the project's dark-mode design system. All animations should use this palette as the foundation.

| Element | Color | Hex (approximate) | Usage |
|---|---|---|---|
| Background | Deep blue-gray | `#0f172a` | All scene backgrounds |
| Surface | Slightly lighter blue-gray | `#1e293b` | Cards, panels, ground planes |
| Primary accent | Bright blue | `#3b82f6` | Manifest glow, active elements, pointers |
| Consent: allowed | Green | `#22c55e` | Unlocked consent toggles, validation success |
| Consent: denied | Red | `#ef4444` | Locked consent toggles, validation failure, expiry |
| Warning / expiring | Amber | `#f59e0b` | TTL countdown in final phase |
| Text (primary) | White | `#f8fafc` | Labels, UMID, shard names |
| Text (secondary) | Muted blue-gray | `#94a3b8` | Descriptions, secondary labels |
| Inactive / expired | Gray | `#475569` | Expired manifests, disabled elements |

---

## Tone and Feel

- **Friendly, modern, slightly playful but not childish.** Think Stripe's documentation animations or Linear's product videos. Clean lines, smooth motion, purposeful transitions.
- **Confident but not aggressive.** The animations should feel like a knowledgeable friend explaining something clearly, not a salesperson pushing a product.
- **Warm technology.** Despite being about data formats and cryptography, the visual language should feel human and approachable. The glow effects, smooth animations, and character interactions keep it warm.
- **Clarity over spectacle.** Every visual element should teach something. Avoid gratuitous effects that don't convey meaning.

---

## Music Direction

- **Genre:** Upbeat electronic, clean and modern
- **Instruments:** Soft synths, clean percussion, subtle bass. No heavy drops or aggressive beats.
- **Tempo:** Medium (100-120 BPM). Energetic but not frantic.
- **Reference mood:** Think "building something cool" -- the feeling of an upbeat tech product launch, not a nightclub. Closer to Tycho or Bonobo than to EDM.
- **Avoid:** Corporate muzak, stock music feel, overly dramatic orchestral, anything with lyrics

---

## Animation Sequences (Suggested)

These are suggested scene structures for explainer animations. Each can be produced as a standalone short or combined into a longer piece.

### Sequence 1: "What Is Universal Manifest?" (30-60 seconds)

1. **Open:** Split screen showing three different apps, each with its own format for a user profile. Arrows between them are tangled, red, frustrated.
2. **Problem statement:** Text overlay -- "Every pair of systems invents a new format."
3. **Transition:** The tangled arrows dissolve. A single manifest card appears in the center, glowing.
4. **Solution:** The manifest opens its shard panels. Clean, blue arrows extend from it to each system. Each system reads the shards it needs.
5. **Close:** The manifest closes, compact again. Text: "One document. Every system."

### Sequence 2: "How Consent Works" (30-45 seconds)

1. **Open:** Riley holds their manifest. Several shard panels are visible, most with red locks.
2. **A system requests access:** A scanning beam reaches toward the manifest.
3. **Denied shards:** The scanner hits a red-locked panel. Flash. Access denied.
4. **Allowed shard:** Riley taps a lock, turning it green. The panel opens, data flows to the requesting system.
5. **Close:** Riley closes the panel, locks it again. Text: "Nothing without your permission."

### Sequence 3: "Offline Tolerance" (30-45 seconds)

1. **Open:** Jordan's gallery, remote location. Wi-Fi icon is crossed out.
2. **Alex arrives:** Alex presents their manifest. Jordan's scanner validates it -- green checkmark.
3. **Time passes:** The TTL timer on Alex's manifest counts down visibly.
4. **Still working:** The gallery display shows Alex's art, sourced from the manifest's shard data. No internet needed.
5. **Expiry:** The timer runs out. The manifest fades to gray. The display politely removes Alex's content.
6. **Close:** Text: "Works offline. Expires on time."

### Sequence 4: "The Resolver" (20-30 seconds)

1. **Open:** Sam at their desk, staring at a UMID string.
2. **Query:** Sam sends the UMID to myum.net. The UMID travels as a glowing packet to the resolver (the locker room).
3. **Lookup:** The correct slot illuminates. The manifest slides out.
4. **Delivery:** The manifest travels back to Sam's screen. Sam reads the shards.
5. **Close:** Text: "Any manifest, anywhere. Just look it up."

### Sequence 5: "Progressive Adoption" (45-60 seconds)

1. **Level 1:** Sam opens a manifest in a basic JSON viewer. "Parse it."
2. **Level 2:** Sam runs a validation check. Green checkmark. "Validate it."
3. **Level 3:** Sam reads a shard and uses the data in their app. "Consume it."
4. **Level 4:** Sam creates their own manifest and publishes it. "Issue it."
5. **Level 5:** Sam signs the manifest (a notary stamp animation). "Sign it."
6. **Close:** The five levels stack up like building blocks. Text: "Start wherever you are."

---

## Technical Notes for Producers

- **Aspect ratio:** Produce at 16:9 for web and presentation use. Consider 1:1 crops for social media.
- **Duration targets:** Individual sequences 20-60 seconds each. Combined overview 2-3 minutes maximum.
- **Text overlays:** Use the project's font system if available. Fallback: clean sans-serif (Inter, SF Pro, or similar).
- **Accessibility:** Ensure sufficient contrast for color-blind viewers. Don't rely solely on red/green to distinguish consent states -- add lock/unlock icons as a secondary signal. Include subtitle tracks for any narration.
- **Export formats:** MP4 (H.264) for web, ProRes for editing, WebM for inline embedding, GIF/APNG for lightweight previews.
