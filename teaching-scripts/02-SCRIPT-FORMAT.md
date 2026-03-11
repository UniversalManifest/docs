# 02 -- Teaching Script Format

## Purpose

This document defines the standard format for writing teaching scripts -- short animated explainers that use the UM Capsule-Pod character to illustrate Universal Manifest concepts. A teaching script is a scene-by-scene blueprint that can be handed to an animator (human or AI) and turned into an SVG animation, a motion graphic, or eventually an interactive sandbox step-through.

---

## Design Principles

1. **Story first, spec second.** Every script tells a story about the Capsule-Pod going somewhere, doing something, encountering a challenge, and resolving it. The viewer learns the concept through the narrative, not through a lecture.

2. **One concept per script.** Each script teaches exactly one idea. If a viewer walks away able to explain that one idea to a friend, the script succeeded.

3. **Show, then name.** Show the visual metaphor first (the pod glowing green), then label it ("That glow means the signature is valid"). Never label first.

4. **Respect the pod vocabulary.** Use the Capsule-Pod shape, the shield overlay, and the prism projection consistently. See 01-ICONIC-REPRESENTATION.md for the full visual system.

5. **Target the "aha" moment.** Every script has exactly one beat where the viewer should think "oh, I get it." The entire script exists to set up and deliver that beat.

---

## Script Metadata Block

Every script file begins with a YAML-style metadata block:

```yaml
---
id: TS-001
title: "What Is a Universal Manifest?"
slug: what-is-um
version: 1
audience: beginner
duration: 30s
concepts:
  - manifest-envelope
  - portable-state
pod-states:
  - resting
  - in-transit
  - verified
palette:
  primary: accent-blue
  secondary: green
related:
  - TS-002
  - TS-005
---
```

### Field Reference

| Field | Required | Description |
|-------|----------|-------------|
| `id` | yes | Unique identifier, format `TS-NNN` |
| `title` | yes | Human-readable title (shown to viewers) |
| `slug` | yes | URL-safe identifier for file naming |
| `version` | yes | Script revision number |
| `audience` | yes | `beginner` / `intermediate` / `advanced` |
| `duration` | yes | Target runtime: `15s`, `30s`, `60s`, or `90s` |
| `concepts` | yes | List of UM concepts this script teaches (from a controlled vocabulary) |
| `pod-states` | yes | Which Capsule-Pod visual states appear in this script |
| `palette` | no | Dominant colors for this script (from the project palette) |
| `related` | no | IDs of scripts that pair well with this one |

---

## Concept Vocabulary

Scripts reference concepts using these controlled terms:

| Term | Meaning |
|------|---------|
| `manifest-envelope` | The core manifest structure (required fields) |
| `portable-state` | The idea that a manifest travels between systems |
| `facets` | Composable named sub-documents |
| `pointers` | URL references to external data |
| `claims` | Roles, permissions, verification assertions |
| `consents` | Per-surface privacy controls |
| `signature-verification` | Ed25519 signature checking (v0.2) |
| `ttl-expiry` | Time-to-live enforcement |
| `forward-compatibility` | Unknown field tolerance |
| `projection` | One manifest, many consumer views |
| `resolution` | UMID lookup via myum.net |
| `tamper-detection` | Detecting modified manifests |
| `revocation` | Checking if a manifest has been invalidated |
| `offline-verification` | Verifying without network access |
| `facet-composition` | Multiple facets coexisting in one manifest |
| `consent-enforcement` | Consumers honoring consent gates |
| `device-enrollment` | IoT/edge device registration |
| `cross-system-handoff` | Manifest moving from one platform to another |

---

## Scene Structure

Each script is divided into **scenes**. Each scene describes one moment in the animation.

### Scene Template

```
## Scene N: [Short Title]

**Duration**: Ns
**Stage**: [What is visible on screen at the start of this scene]
**Action**: [What happens during this scene -- movements, transformations, reveals]
**Pod state**: [The Capsule-Pod's visual state during this scene]
**Text overlay**: [Any text that appears on screen, with position]
**Callout**: [Optional speech bubble or annotation, with pointer target]
**Transition**: [How this scene flows into the next -- cut, fade, slide, morph]
**Beat**: [The emotional/conceptual beat -- what the viewer feels or understands]
```

### Scene Fields Explained

**Duration**: How many seconds this scene lasts. The sum of all scene durations should equal the script's total duration (within 1-2 seconds for transition overlap).

**Stage**: A declarative description of what is on screen when the scene begins. Include positions (left, center, right), which elements are present, and their current states.

**Action**: A step-by-step description of what happens. Use active verbs: "The pod slides left to right," "The shield overlay fades in," "A callout bubble rises from the pod."

**Pod state**: One of the states from the visual vocabulary: `resting`, `in-transit`, `verified`, `rejected`, `projecting`, `expiring`, `expired`, `being-created`. This determines the pod's color scheme for the scene.

**Text overlay**: Any words that appear on screen. Specify:
- The text content
- Position (`top-center`, `bottom-left`, `beside-pod`, etc.)
- Style (`title`, `subtitle`, `label`, `mono` for code-like text)
- Timing (`appears at 0.5s`, `fades in over 0.3s`)

**Callout**: An optional annotation bubble with a pointer (arrow or line) connecting it to a specific element. Specify the callout text, the target element, and the bubble position.

**Transition**: How this scene connects to the next:
- `cut` -- instant switch
- `fade` -- cross-dissolve
- `slide-left` / `slide-right` -- scene slides out, next slides in
- `morph` -- elements transform smoothly into the next scene's layout
- `zoom-in` / `zoom-out` -- camera moves

**Beat**: A one-sentence description of the conceptual or emotional purpose of this scene. This is the "director's note" -- it tells the animator what the viewer should feel, not just what they should see.

---

## Complete Example Script

```
---
id: TS-001
title: "What Is a Universal Manifest?"
slug: what-is-um
version: 1
audience: beginner
duration: 30s
concepts:
  - manifest-envelope
  - portable-state
pod-states:
  - being-created
  - resting
  - in-transit
  - verified
palette:
  primary: accent-blue
  secondary: green
related:
  - TS-002
  - TS-003
---

## Scene 1: Empty Space

**Duration**: 3s
**Stage**: Dark background (#0f172a). Nothing on screen except a faint grid
  of dots suggesting a digital substrate.
**Action**: A small, bright point of light appears at center screen and
  begins to expand.
**Pod state**: being-created
**Text overlay**: None
**Callout**: None
**Transition**: morph (the light expands into the pod shape)
**Beat**: Anticipation. Something is forming.

## Scene 2: The Pod Appears

**Duration**: 5s
**Stage**: The light has resolved into the Capsule-Pod shape at center
  screen. The outer shell is accent-blue (#3b82f6). The inner payload
  area shows a subtle UM mark. The gap between shell and payload is
  dark (resting state).
**Action**: The pod completes its formation with a gentle pulse. Small
  label elements fade in around it: "@id" at top, "subject" at left,
  "issuedAt" at right, "expiresAt" at bottom. These labels orbit
  briefly then settle into positions.
**Pod state**: resting
**Text overlay**:
  - "Universal Manifest" -- top-center, title style, appears at 1s
  - "A portable state capsule" -- below title, subtitle style, appears at 2.5s
**Callout**: None
**Transition**: fade
**Beat**: Introduction. The viewer sees the shape for the first time
  and learns its name.

## Scene 3: Two Systems Appear

**Duration**: 4s
**Stage**: The pod is at center. Two system icons (rounded rectangles
  with simple logos) fade in: "App A" on the far left, "App B" on the
  far right. A dotted line connects them through the center where the
  pod sits.
**Action**: The system icons fade in with a gentle scale-up. The dotted
  line draws itself from left to right. The pod bobs gently at center.
**Pod state**: resting
**Text overlay**: None
**Callout**:
  - "App A needs to send state to App B" -- bottom-center, label style
**Transition**: morph
**Beat**: Setup. The viewer understands the scenario: two systems
  need to communicate.

## Scene 4: The Pod Travels

**Duration**: 6s
**Stage**: Pod at center, App A on left, App B on right, dotted line
  connecting them.
**Action**: The pod shifts to the left, docks briefly with App A (a
  brief blue pulse at the connection point). Then the pod launches
  rightward along the dotted line. As it travels, the gap between
  shell and payload glows faint blue (in-transit state). The pod
  arrives at App B and docks (another blue pulse).
**Pod state**: in-transit
**Text overlay**:
  - "The manifest travels" -- top-center, subtitle style, appears at 1s
**Callout**: None
**Transition**: morph
**Beat**: The "aha" moment. The manifest IS the transport mechanism.
  It is not an API call, not a database sync -- it is a document that
  physically moves.

## Scene 5: Verification

**Duration**: 5s
**Stage**: Pod has arrived at App B on the right side. App B's icon
  is highlighted.
**Action**: App B sends a scanning beam across the pod (a horizontal
  line of light sweeping left to right across the pod surface). The
  gap between shell and payload illuminates green. A small shield
  icon appears above the pod and fades in. A checkmark appears inside
  the pod's inner payload area.
**Pod state**: verified
**Text overlay**:
  - "Verified." -- beside the pod (right), label style, appears at 3s
**Callout**:
  - "Signature valid. Contents intact." -- below pod, label style
**Transition**: fade
**Beat**: Trust. The receiving system confirmed the manifest is genuine
  without calling home to any central server.

## Scene 6: Resolution

**Duration**: 4s
**Stage**: Pod at App B, verified state (green glow). Both systems
  visible.
**Action**: The field labels from Scene 2 reappear around the pod,
  but now they show real values: a UUID for @id, a DID for subject,
  timestamps for issuedAt/expiresAt. The labels glow softly.
**Pod state**: verified
**Text overlay**:
  - "One document. Any system." -- bottom-center, title style, appears at 1s
**Callout**: None
**Transition**: fade to dark
**Beat**: The payoff. The viewer understands the core value
  proposition: a single, portable, verifiable document that any
  system can read.

## Scene 7: End Card

**Duration**: 3s
**Stage**: Dark background. The pod shape fades to a small, resting
  icon at center.
**Action**: The text "universalmanifest.net" fades in below the pod
  icon.
**Pod state**: resting
**Text overlay**:
  - "universalmanifest.net" -- center, mono style
**Callout**: None
**Transition**: fade to black
**Beat**: Brand imprint. The viewer knows where to learn more.
```

---

## Production Notes Section

Each script should end with a `## Production Notes` section that provides guidance for the animator:

```
## Production Notes

### Key Animation Details
- [Specific timing notes, easing curves, or motion details]
- [Color transition specifics]
- [Interaction between elements]

### Accessibility
- [Alt text for the overall animation]
- [Reduced-motion fallback description]
- [Color contrast considerations]

### SVG Implementation Hints
- [Suggested SVG structure: groups, layers, animation approach]
- [Whether CSS animations or SMIL is preferred]
- [Reusable components from existing animation library]

### Sandbox Integration
- [How this script maps to the interactive sandbox step-through]
- [Which steps become interactive breakpoints]
- [What the user can modify at each step]
```

---

## File Naming Convention

Teaching scripts live in `/docs/teaching-scripts/scripts/` and follow this naming pattern:

```
TS-001-what-is-um.md
TS-002-inside-the-pod.md
TS-003-watch-it-travel.md
```

Format: `TS-{NNN}-{slug}.md`

---

## Checklist Before Submitting a Script

- [ ] Metadata block is complete with all required fields
- [ ] Total scene durations sum to the declared duration (within 2s)
- [ ] Every scene has all seven fields filled in
- [ ] The pod state is specified for every scene
- [ ] There is exactly one "aha" beat identified in the script
- [ ] Concepts listed in metadata are actually demonstrated in the scenes
- [ ] Production notes section is present
- [ ] The script has been read aloud to check pacing (1 scene = ~1 breath)
