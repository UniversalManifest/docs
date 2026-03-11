# 01 -- Iconic Representation for Universal Manifest

## The Design Challenge

Universal Manifest needs a single, instantly recognizable visual form -- a **character** that can travel through every teaching animation, every explainer, every diagram. This shape is the UM's "mascot" in the same way that a padlock icon means security, an envelope icon means email, or a cloud icon means remote storage.

The shape must work as:
- A tiny favicon (16x16)
- An inline icon in text (24px)
- A mid-size element traveling through animated scenes (60-120px)
- A hero illustration centerpiece (400px+)

It must visually communicate:
- **Containment** -- it holds things inside
- **Portability** -- it moves between places
- **Trust** -- it carries guarantees
- **Openness** -- its contents can be read/projected by anyone who understands the format
- **Liveliness** -- it is not static data; it has a TTL, it expires, it gets verified

It must support these animation states:
- **Traveling** -- moving between systems
- **Being verified** -- signature check (glow, shield overlay, checkmark reveal)
- **Being projected** -- facets/pointers extracting outward (opening, radiating)
- **Expiring** -- TTL countdown, fade/dissolve
- **Being created** -- assembly, sealing
- **Being rejected** -- tamper detected, red flash, crack/shatter

---

## Candidate Concepts

### Concept 1: The Capsule (Rounded Pill)

```
    ╭─────────────╮
    │             │
    │   ╭─────╮  │
    │   │ UM  │  │
    │   ╰─────╯  │
    │             │
    ╰─────────────╯
```

**Shape**: A horizontally-oriented rounded rectangle (pill shape) with slightly convex top and bottom edges, like a pharmaceutical capsule or a USB stick. The interior has a subtle inner border suggesting "walls" around the payload.

**Visual metaphor**: A capsule is something you swallow whole -- self-contained, designed for transport, carries something valuable inside. The medical capsule metaphor also suggests precision and reliability.

**Traveling**: Slides smoothly between systems on a horizontal track, slight rotation possible. The pill shape implies directionality (it's going somewhere).

**Verification**: A translucent shield shimmer sweeps across the capsule surface, then a green glow emanates from the inner border. The capsule briefly becomes transparent to show a checkmark inside.

**Projection**: The capsule splits at a seam (like opening a pill), and facet elements float outward. The two halves stay connected by thin lines.

**Rating**:
- Simplicity: 8/10 -- very simple shape, easy to draw at any size
- Distinctiveness: 5/10 -- pill shapes are common; might be confused with a button or badge
- Metaphor strength: 7/10 -- "capsule" directly maps to "state capsule"
- Animation-friendliness: 8/10 -- smooth curves animate well, the split-open gesture is natural

---

### Concept 2: The Sealed Envelope with Wax Seal

```
        ╱╲
       ╱  ╲
      ╱    ╲
    ╭╱──────╲╮
    │        │
    │   ⊙    │
    │        │
    ╰────────╯
```

**Shape**: A classic envelope shape viewed from the front -- rectangular body with a triangular flap on top. At the center of the flap/body junction sits a circular wax seal (the UM seal). The seal is the focal point; the envelope is the carrier.

**Visual metaphor**: A sealed letter is the oldest metaphor for trusted, portable information. The wax seal carries the authority of the issuer. Opening the envelope reveals the contents. The seal proves it has not been tampered with.

**Traveling**: The envelope glides between systems, the wax seal glinting. A slight tilt gives it the feeling of being handed from one entity to another.

**Verification**: The wax seal pulses, then a magnifying glass or scanner beam sweeps over it. The seal flashes green if valid, cracks and turns red if tampered.

**Projection**: The flap lifts up, and facet elements rise out of the open envelope like documents being fanned out. Pointer arrows extend from the envelope edges.

**Rating**:
- Simplicity: 6/10 -- more visual detail than minimal shapes; the seal adds complexity
- Distinctiveness: 7/10 -- evocative and recognizable, but "envelope" is overloaded (email)
- Metaphor strength: 9/10 -- directly maps to portable, sealed, verifiable document
- Animation-friendliness: 7/10 -- the opening flap and seal verification animate beautifully

---

### Concept 3: The Faceted Gem / Crystal

```
       ╱╲
      ╱  ╲
     ╱ ╱╲ ╲
    ╱ ╱  ╲ ╲
    ╲ ╲  ╱ ╱
     ╲ ╲╱ ╱
      ╲  ╱
       ╲╱
```

**Shape**: A hexagonal or octagonal gem shape, viewed from above, with internal facet lines suggesting crystalline structure. The facets represent the different sections of a manifest (header, facets, claims, consents, pointers). The whole gem has a subtle internal glow.

**Visual metaphor**: A gem is compact, valuable, internally structured, and durable. The facets suggest multiple faces/views (projection). Light passing through a gem creates different colors depending on the angle -- just as different consumers see different projections of the same manifest.

**Traveling**: Rotates slowly as it moves, catching light on different facets. The rotation suggests dimensionality.

**Verification**: The gem pulses with internal light, each facet briefly illuminating in sequence. A verified gem glows with a steady, pure light. A tampered gem shows a visible crack through one facet.

**Projection**: Individual facets detach slightly and float outward, each representing a facet or pointer. The core gem remains intact while projections radiate.

**Rating**:
- Simplicity: 5/10 -- facet lines add detail that may not read at small sizes
- Distinctiveness: 8/10 -- uncommon in tech iconography; memorable
- Metaphor strength: 7/10 -- "multi-faceted" is a stretch; gems are not inherently about portability
- Animation-friendliness: 6/10 -- rotation and facet lighting are CPU-intensive in SVG

---

### Concept 4: The Hexagonal Token / Coin

```
      ╱──╲
     ╱    ╲
    │  UM  │
     ╲    ╱
      ╲──╱
```

**Shape**: A flat hexagon (regular six-sided polygon) with a subtle bevel or depth effect suggesting a physical token or coin. The center carries the UM mark. The hexagonal shape references the honeycomb pattern, suggesting modular composition and tessellation.

**Visual metaphor**: A token is something you carry and present. It grants access, proves membership, or carries stored value. Hexagons tessellate -- they fit together without gaps -- which maps to composability. The coin metaphor suggests currency of trust.

**Traveling**: Flips or spins edge-over-edge as it moves, like a coin toss. The flat shape makes it easy to slot into different systems (docking gesture).

**Verification**: The coin flips to reveal a second face -- the "verified" face shows a green checkmark or shield. The two-faced nature maps to signed/unsigned states.

**Projection**: Hex segments separate outward like a honeycomb exploding, each segment carrying a facet or pointer label. The center remains as the core envelope.

**Rating**:
- Simplicity: 9/10 -- hexagon is trivially simple; reads at any size
- Distinctiveness: 6/10 -- hexagons are everywhere in tech branding
- Metaphor strength: 6/10 -- token/coin works but is not strongly tied to "portable state"
- Animation-friendliness: 9/10 -- flat polygon is the easiest shape to animate in SVG

---

### Concept 5: The Orb with Orbit Rings

```
        ─ ─
      /     \
    ──(  UM  )──
      \     /
        ─ ─
```

**Shape**: A sphere (drawn as a circle with shading to suggest 3D) surrounded by one or two orbital ellipses, like an atom or a planet with rings. The orb is the manifest core; the rings represent the layers (claims, consents, facets, pointers) orbiting around it.

**Visual metaphor**: An atom contains structured matter in a compact form. The orbital rings suggest energy, dynamism, and layers of structure. The contained-yet-active nature maps well to a living document with a TTL.

**Traveling**: The orb glides smoothly, rings spinning. The orbital motion gives a sense of internal activity even when stationary.

**Verification**: The rings lock into alignment (like a combination lock clicking), and the orb pulses green. Failed verification shows rings jittering out of alignment.

**Projection**: Rings expand outward, each ring segment becoming a facet or pointer label that floats to its destination.

**Rating**:
- Simplicity: 6/10 -- the orbit rings add complexity
- Distinctiveness: 7/10 -- atom/orbit is recognizable but has science connotations
- Metaphor strength: 7/10 -- layered structure maps to manifest layers; dynamism maps to TTL
- Animation-friendliness: 7/10 -- orbit animation is well-established but needs careful SVG work

---

### Concept 6: The Shield-Badge

```
      ╭──────╮
     ╱        ╲
    │    UM    │
    │          │
     ╲        ╱
      ╲      ╱
       ╲    ╱
        ╲  ╱
         ╲╱
```

**Shape**: A shield shape (heraldic, pointed at the bottom) with a clean interior area for the UM mark. The shield has a subtle double-border suggesting an inner and outer layer. The overall form suggests protection, authority, and official credential.

**Visual metaphor**: A shield protects and authenticates. Badges and shields are used on passports, credentials, and certificates. The pointed bottom gives directionality (it can "point" toward destinations). The double border suggests the envelope-around-payload structure.

**Traveling**: Moves with the pointed end forward, like an arrowhead. Slight bounce or hover animation while in transit.

**Verification**: The inner area glows, and a checkmark or lock icon appears inside. The double border pulses with light traveling along it (a verification sweep).

**Projection**: The shield opens like a book (hinged at the top), revealing facet elements stacked inside. Or: the shield becomes semi-transparent, and labeled layers separate vertically.

**Rating**:
- Simplicity: 7/10 -- shield is recognizable; works at small sizes but the pointed bottom adds detail
- Distinctiveness: 7/10 -- shields are common in security branding but not in data portability
- Metaphor strength: 8/10 -- directly maps to trust, authority, and credential portability
- Animation-friendliness: 7/10 -- shield is easy to draw; opening/revealing animations work well

---

### Concept 7: The Manifest Scroll (Rolled Document)

```
    ╭═╗─────────╔═╮
    │ ║         ║ │
    │ ║  ≡ UM  ║ │
    │ ║         ║ │
    ╰═╝─────────╚═╯
```

**Shape**: A document/scroll viewed from the front, with rolled edges on the left and right suggesting a scroll that can be unfurled. The center shows content lines (like text). The rolled edges give it a 3D feel. Small enough to work as an icon, distinctive enough to stand out.

**Visual metaphor**: A scroll is the original portable document. It can be sealed (rolled shut), opened for reading, carried between kingdoms, and verified by its seal. The unfurling action maps to projection/consumption.

**Traveling**: Rolls along its path, or glides with a slight wobble suggesting the weight of its contents.

**Verification**: A seal appears on the scroll's surface, glows, and resolves to a checkmark. The scroll's edges tighten (the roll becomes tighter) to indicate integrity.

**Projection**: The scroll unfurls in both directions, revealing layered content sections. Facets peel off as individual mini-scrolls.

**Rating**:
- Simplicity: 6/10 -- the rolled edges add drawing complexity at small sizes
- Distinctiveness: 7/10 -- scroll metaphor is strong but visually complex
- Metaphor strength: 8/10 -- directly maps to portable, verifiable, openable document
- Animation-friendliness: 6/10 -- unfurling animation is charming but technically demanding

---

### Concept 8: The Nested Bracket / Container

```
    ╭───────────────╮
    │ ╭───────────╮ │
    │ │ ╭───────╮ │ │
    │ │ │  UM   │ │ │
    │ │ ╰───────╯ │ │
    │ ╰───────────╯ │
    ╰───────────────╯
```

**Shape**: Three concentric rounded rectangles, each slightly smaller than the one containing it. The outermost is the envelope, the middle is the integrity layer, the innermost is the payload. The layers can be drawn with different colors (blue, amber, green) matching the existing animation palette. Minimal and geometric.

**Visual metaphor**: Nesting directly represents the manifest's layered structure -- envelope wrapping integrity wrapping payload. The "Russian doll" or "onion layers" metaphor shows that the manifest is structured in predictable layers that you peel back.

**Traveling**: The nested shape moves as one unit, but the layers subtly oscillate (inner layers lag behind outer layers) to suggest contents sloshing gently.

**Verification**: Each layer lights up sequentially from outside in (envelope check, integrity check, payload check). Green pulse when all three pass.

**Projection**: The layers separate vertically or explode outward concentrically, each layer revealing its labeled contents.

**Rating**:
- Simplicity: 8/10 -- concentric rectangles are trivially simple
- Distinctiveness: 5/10 -- nested rectangles are generic; could be mistaken for a UI wireframe
- Metaphor strength: 8/10 -- layered containment directly maps to manifest structure
- Animation-friendliness: 9/10 -- layer separation and sequential lighting are easy in CSS/SVG

---

### Concept 9: The Prism / Faceted Lens

```
         ╱╲
        ╱  ╲
       ╱    ╲
      ╱  UM  ╲
     ╱        ╲
    ╱──────────╲
```

**Shape**: A triangular prism (drawn as an equilateral triangle with subtle shading to suggest depth). The key visual gimmick: a single beam of light enters one side, and multiple colored beams exit the other side -- the classic Pink Floyd prism effect. The entering beam is the raw manifest; the exiting beams are the projections (different consumers seeing different parts).

**Visual metaphor**: A prism takes one input and produces multiple outputs without losing information. This perfectly maps to UM's projection model: one manifest, many consumer views. The prism is also optically pure (transparent, trust-worthy) and geometrically precise.

**Traveling**: The triangle glides with the pointed end forward, a subtle rainbow shimmer along its edges.

**Verification**: The prism becomes more transparent/clear (verified = optically pure). Tampered = cloudy/cracked, light scatters instead of refracting cleanly.

**Projection**: The signature prism move -- a white beam enters, splits into colored beams (each labeled with a consumer type: social, IoT, spatial, etc.).

**Rating**:
- Simplicity: 7/10 -- triangle is simple; the refraction effect adds detail
- Distinctiveness: 9/10 -- instantly recognizable, visually stunning, uncommon in tech branding
- Metaphor strength: 9/10 -- projection model maps perfectly to prism refraction
- Animation-friendliness: 7/10 -- the refraction effect is gorgeous but needs careful SVG gradients

---

### Concept 10: The Compass Rose / Waypoint Marker

```
          ╱╲
         ╱  ╲
    ╲   ╱    ╲   ╱
     ╲ ╱  UM  ╲ ╱
      ╳        ╳
     ╱ ╲      ╱ ╲
    ╱   ╲    ╱   ╲
         ╲  ╱
          ╲╱
```

**Shape**: A four-pointed compass star with a circular center. The four points suggest four cardinal directions (or the four key manifest sections: claims, consents, facets, pointers). The circular center carries the UM mark. The overall shape suggests navigation, direction, and destination-finding.

**Visual metaphor**: A compass helps you navigate. The manifest is a navigational document -- it tells systems where to find data (pointers), what permissions exist (consents), what claims are made, and what payloads are available (facets). The compass rose also suggests the manifest works in all directions -- any system can read it.

**Traveling**: Rotates slowly as it moves, the compass points suggesting it is orienting to its new environment.

**Verification**: The center circle pulses; the four points glow sequentially as each section is validated.

**Projection**: Each compass point extends outward, becoming a labeled arrow pointing to a consumer system. The center stays fixed as the navigational hub.

**Rating**:
- Simplicity: 5/10 -- the four points add visual complexity
- Distinctiveness: 7/10 -- compass rose is distinctive but may suggest "location" more than "identity"
- Metaphor strength: 6/10 -- navigation is a secondary metaphor; "portable state" is primary
- Animation-friendliness: 7/10 -- rotation and point-extension animate well

---

### Concept 11: The Capsule-Pod (Rounded Hexagonal Container)

```
      ╭────────╮
     ╱  ╭────╮  ╲
    │   │ UM │   │
     ╲  ╰────╯  ╱
      ╰────────╯
```

**Shape**: A hybrid between a hexagonal token and a capsule -- a vertically-oriented rounded hexagon (like a slightly squashed circle with flat top and bottom) containing an inner rounded rectangle (the payload). The outer shape is the envelope; the inner shape is the data. There is visible "space" between the two, suggesting a protective shell around precious cargo.

**Visual metaphor**: A pod (like an escape pod, a seed pod, or a data pod) is self-contained, designed for transport through hostile environments, and opens to release its contents at the destination. The gap between outer shell and inner payload suggests the integrity/signature layer -- the protective padding.

**Traveling**: Moves with a gentle bobbing motion, like a pod floating through space or water. The shell slightly flexes as it accelerates.

**Verification**: The gap between shell and payload illuminates (green for valid, red for tampered). This directly visualizes the integrity layer being checked.

**Projection**: The outer shell peels open (like a seed pod), and facet elements emerge and float toward their destinations. The inner payload stays visible as the source.

**Rating**:
- Simplicity: 7/10 -- two concentric shapes is relatively simple
- Distinctiveness: 8/10 -- the double-shell-with-gap is unusual and memorable
- Metaphor strength: 9/10 -- pod = portable container with protective shell = manifest with integrity layer
- Animation-friendliness: 8/10 -- the shell-open and gap-illumination gestures are elegant and easy

---

### Concept 12: The Keystone (Arch Wedge)

```
    ╭──────────────╮
    │              │
    │      UM      │
    │              │
    ╰──╮        ╭──╯
       │        │
       ╰────────╯
```

**Shape**: A trapezoidal "keystone" shape -- wider at the top, narrower at the bottom, like the central stone in an arch. The keystone is the structural element that holds an arch together. Without it, the whole structure collapses.

**Visual metaphor**: A keystone is the critical piece that makes everything else work. The manifest is the keystone of interoperability -- without it, systems cannot exchange state. The trapezoidal shape also suggests it "locks in" to different architectures (it slots into gaps between systems).

**Traveling**: Slots into position at each destination, like a puzzle piece finding its place. Travels with a slight rotation to show it is looking for where it fits.

**Verification**: The keystone glows and "locks" into place with a satisfying click/pulse. The surrounding arch structure materializes to show the manifest enabling the connection.

**Projection**: Layers separate downward from the wider top, like geological strata.

**Rating**:
- Simplicity: 7/10 -- trapezoid is simple but less immediately recognizable
- Distinctiveness: 8/10 -- keystone shape is rare in tech; carries strong architectural metaphor
- Metaphor strength: 7/10 -- "critical connecting piece" is a secondary metaphor for UM
- Animation-friendliness: 7/10 -- the "slotting in" gesture is satisfying but requires context (the arch)

---

## Comparative Summary

| # | Concept | Simplicity | Distinctiveness | Metaphor | Animation | **Total** |
|---|---------|-----------|----------------|----------|-----------|-----------|
| 1 | Capsule (Pill) | 8 | 5 | 7 | 8 | 28 |
| 2 | Sealed Envelope | 6 | 7 | 9 | 7 | 29 |
| 3 | Faceted Gem | 5 | 8 | 7 | 6 | 26 |
| 4 | Hexagonal Token | 9 | 6 | 6 | 9 | 30 |
| 5 | Orb with Orbits | 6 | 7 | 7 | 7 | 27 |
| 6 | Shield-Badge | 7 | 7 | 8 | 7 | 29 |
| 7 | Manifest Scroll | 6 | 7 | 8 | 6 | 27 |
| 8 | Nested Brackets | 8 | 5 | 8 | 9 | 30 |
| 9 | Prism | 7 | 9 | 9 | 7 | 32 |
| 10 | Compass Rose | 5 | 7 | 6 | 7 | 25 |
| 11 | Capsule-Pod | 7 | 8 | 9 | 8 | 32 |
| 12 | Keystone | 7 | 8 | 7 | 7 | 29 |

---

## Recommended Top 3

### First Choice: The Capsule-Pod (Concept 11)

**Why it wins**: The Capsule-Pod is the strongest overall match for what Universal Manifest actually is. The name itself -- "state capsule" -- maps directly to the pod shape. The visible gap between outer shell and inner payload is a brilliant visual metaphor for the integrity/signature layer, and it creates the single most important animation beat: **the gap lights up during verification**. That one gesture -- the protective layer illuminating green or red -- instantly teaches the viewer what verification means without a single word of explanation.

The pod metaphor also supports every animation state naturally:
- **Traveling**: pods float, drift, get handed off -- all natural motions
- **Verification**: the gap between shell and payload illuminates
- **Projection**: the shell opens like a seed pod, contents emerge
- **Expiring**: the shell slowly becomes translucent, then shatters like glass
- **Creation**: the payload forms first, then the shell wraps around it, then the seal is applied
- **Rejection**: a crack appears in the shell, red light leaks through the gap

The double-contour shape (shell + payload) also gives us a **built-in visual hierarchy** that reads at every size:
- At favicon size: a single rounded shape with a visible inner dot
- At icon size: the shell-gap-payload structure is clear
- At hero size: full detail with labels, glow effects, and animated sections

**Recommended form details**:
- Outer shell: rounded hexagonal or elliptical, drawn with a 2px stroke in the accent blue (`#3b82f6`)
- Inner payload: smaller rounded rectangle, filled with card color (`#1e293b`)
- Gap: transparent, but lights up with color during state changes
- UM mark: centered in the inner payload, using the project's monospace font
- Default state: the gap is a subtle dark border; the shape is calm, cool, resting
- In motion: the gap shows a faint blue pulse, like a heartbeat

```
  RESTING STATE          VERIFIED STATE         PROJECTION STATE

  ╭──────────╮          ╭──────────╮           ╭──  ────  ──╮
 ╱  ┌──────┐  ╲       ╱░░┌──────┐░░╲         ╱  ┌──────┐    ╲
│   │      │   │     │░░░│  ✓   │░░░│       │   │ facet│───→  │
│   │  UM  │   │     │░░░│  UM  │░░░│       │   │  UM  │───→  │
│   │      │   │     │░░░│      │░░░│       │   │ ptr  │───→  │
 ╲  └──────┘  ╱       ╲░░└──────┘░░╱         ╲  └──────┘    ╱
  ╰──────────╯          ╰──────────╯           ╰──  ────  ──╯
                         (green glow)          (shell opens,
                                                arrows emerge)
```

### Second Choice: The Prism (Concept 9)

**Why it is strong**: The prism is the most visually distinctive concept and perfectly captures UM's projection model -- one manifest in, many consumer views out. The "white light splits into a spectrum" animation is instantly understood by anyone who has seen the classic physics demonstration (or the Pink Floyd album cover). This makes the projection concept effortless to teach.

The prism also carries a strong metaphor for trust: a pure, flawless prism refracts light cleanly; a cracked or cloudy prism distorts the output. Verification = optical purity.

**Why it is second, not first**: The prism excels at explaining projection but is weaker for the other animation states. A prism does not naturally "travel" between systems the way a capsule does. It does not obviously "contain" facets. And at small sizes, a triangle is less distinctive than a pod shape. The prism works best as a **secondary visual metaphor** used in specific scenes (the projection/consumption scene) rather than as the primary traveling character.

**Recommended use**: The prism should appear as a **transformation scene** -- the pod arrives at a consumer, enters a prism, and the consumer's specific projection emerges from the other side. The prism is the consumer's lens, not the manifest itself.

### Third Choice: The Shield-Badge (Concept 6)

**Why it is strong**: The shield directly communicates trust and authority, which are central to UM's value proposition. Shields are universally understood as protection symbols. The pointed-bottom shape gives directionality for travel animations. The double-border naturally maps to envelope + integrity layer.

**Why it is third**: The shield's weakness is that it overemphasizes the security/trust aspect at the expense of portability and openness. A viewer might think "this is about security" rather than "this is about portable state." Additionally, shield shapes are heavily used in security product branding (VPNs, antivirus, password managers), which could cause confusion about what UM is.

**Recommended use**: The shield should appear as a **state overlay** -- when a manifest is verified, a small shield icon briefly appears on top of the pod to indicate "integrity confirmed." The shield is the verification badge, not the manifest itself.

---

## Recommended Visual System

The teaching scripts should use all three concepts in a layered visual system:

| Element | Shape | Role |
|---------|-------|------|
| **The Manifest** | Capsule-Pod | The main character; travels, gets created, expires |
| **Verification** | Shield overlay on the pod | Appears during/after signature check |
| **Projection** | Prism at consumer side | Transforms the pod into consumer-specific views |

This gives us a consistent visual vocabulary:
- "When you see the **pod**, that is the manifest."
- "When you see the **shield glow**, the manifest has been verified."
- "When you see the **prism split**, the consumer is extracting what it needs."

---

## Color Mapping (Aligned with Existing Animation Palette)

The Capsule-Pod should use the project's established color palette from the existing SVG animations:

| Pod State | Shell Color | Gap Color | Payload Color |
|-----------|-------------|-----------|---------------|
| Resting/Idle | `#334155` (border) | transparent | `#1e293b` (card) |
| In Transit | `#3b82f6` (accent blue) | faint blue pulse | `#1e293b` |
| Verified | `#22c55e` (green) | green glow | `#1e293b` |
| Rejected/Tampered | `#ef4444` (red) | red warning glow | `#1e293b` with crack |
| Projecting | `#8b5cf6` (violet) | violet shimmer | `#1e293b` opening |
| Expiring | `#f59e0b` (amber) | amber fade | `#1e293b` fading |
| Expired/Dead | `#64748b` (grey) | none | `#0f172a` (bg) |

---

## Size Reference

```
FAVICON (16px)          ICON (32px)           INLINE (64px)

    ╭──╮               ╭──────╮              ╭──────────╮
    │▪│               │ ┌──┐ │             ╱  ┌──────┐  ╲
    ╰──╯               │ └──┘ │            │   │  UM  │   │
                        ╰──────╯             ╲  └──────┘  ╱
                                              ╰──────────╯

CARD (128px)                           HERO (256px+)

    ╭──────────────╮                  ╭──────────────────────╮
   ╱  ╭──────────╮  ╲               ╱    ╭────────────────╮    ╲
  │   │          │   │             │     │                │     │
  │   │    UM    │   │             │     │   Universal    │     │
  │   │          │   │             │     │   Manifest     │     │
   ╲  ╰──────────╯  ╱               ╲    ╰────────────────╯    ╱
    ╰──────────────╯                  ╰──────────────────────╯
```

---

## Next Step

Once the iconic representation is approved, the next stage is to define the animation script format (02-SCRIPT-FORMAT.md) that uses this visual vocabulary to tell stories about the Capsule-Pod character traveling through Universal Manifest scenarios.
