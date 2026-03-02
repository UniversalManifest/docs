# Capsule-Pod Design -- Approved Iconic Representation

**Status**: Approved (2026-02-28, CEO decision)
**Source**: Concept 11 from [01-ICONIC-REPRESENTATION.md](../teaching-scripts/01-ICONIC-REPRESENTATION.md)

---

## Summary

The **Capsule-Pod** is the approved iconic visual character for Universal Manifest. It scored joint-highest (32/40) in the comparative analysis of 12 candidate concepts, and was selected for its direct metaphor mapping to the manifest's core structure: a protective outer shell with a visible gap (integrity layer) around a payload core.

The name "state capsule" maps directly to the pod shape. The visible gap between outer shell and inner payload is the defining visual feature -- it illuminates during verification (green = valid, red = tampered), instantly teaching the viewer what verification means without words.

---

## Structural Anatomy

```
      ╭────────╮
     ╱  ╭────╮  ╲       Shell  = envelope (outer boundary)
    │   │ UM │   │       Gap    = integrity/signature layer
     ╲  ╰────╯  ╱       Payload = manifest data core
      ╰────────╯
```

Three concentric zones:

| Zone | Maps to | Visual Role |
|------|---------|-------------|
| **Shell** (outer) | Envelope boundary | Protective container; carries the pod through transit |
| **Gap** (between) | Integrity / signature layer | Illuminates during verification; the key animation beat |
| **Payload** (inner) | Claims, shards, pointers, consents | The carried data; revealed during projection |

---

## Animation States

```
  RESTING STATE          VERIFIED STATE         PROJECTION STATE

  ╭──────────╮          ╭──────────╮           ╭──  ────  ──╮
 ╱  ┌──────┐  ╲       ╱░░┌──────┐░░╲         ╱  ┌──────┐    ╲
│   │      │   │     │░░░│  ✓   │░░░│       │   │ shard│───→  │
│   │  UM  │   │     │░░░│  UM  │░░░│       │   │  UM  │───→  │
│   │      │   │     │░░░│      │░░░│       │   │ ptr  │───→  │
 ╲  └──────┘  ╱       ╲░░└──────┘░░╱         ╲  └──────┘    ╱
  ╰──────────╯          ╰──────────╯           ╰──  ────  ──╯
                         (green glow)          (shell opens,
                                                arrows emerge)
```

| State | Animation Beat |
|-------|---------------|
| **Resting / Idle** | Calm, cool, subtle dark border gap |
| **In Transit** | Gentle bobbing motion; faint blue pulse in the gap |
| **Verified** | Gap illuminates green; checkmark appears in payload |
| **Rejected / Tampered** | Crack appears in shell; red light leaks through gap |
| **Projecting** | Shell peels open (seed-pod gesture); shard elements emerge |
| **Expiring** | Shell becomes translucent; amber countdown; eventual shatter |
| **Creation** | Payload forms first, shell wraps around it, seal applied |

---

## Visual System

The teaching scripts use three visual concepts in a layered system. The Capsule-Pod is the primary character; the other two appear as contextual overlays.

| Element | Shape | Role |
|---------|-------|------|
| **The Manifest** | Capsule-Pod | The main character; travels, gets created, expires |
| **Verification** | Shield overlay on the pod | Appears during/after signature check |
| **Projection** | Prism at consumer side | Transforms the pod into consumer-specific views |

Visual vocabulary:

- "When you see the **pod**, that is the manifest."
- "When you see the **shield glow**, the manifest has been verified."
- "When you see the **prism split**, the consumer is extracting what it needs."

---

## Color Mapping

Aligned with the project's established animation palette (dark-theme, `#0f172a` background):

| Pod State | Shell Color | Gap Color | Payload Color |
|-----------|-------------|-----------|---------------|
| Resting / Idle | `#334155` (border) | transparent | `#1e293b` (card) |
| In Transit | `#3b82f6` (accent blue) | faint blue pulse | `#1e293b` |
| Verified | `#22c55e` (green) | green glow | `#1e293b` |
| Rejected / Tampered | `#ef4444` (red) | red warning glow | `#1e293b` with crack |
| Projecting | `#8b5cf6` (violet) | violet shimmer | `#1e293b` opening |
| Expiring | `#f59e0b` (amber) | amber fade | `#1e293b` fading |
| Expired / Dead | `#64748b` (grey) | none | `#0f172a` (bg) |

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

Recommended form details at render scale:

- **Outer shell**: rounded hexagonal or elliptical, 2px stroke in accent blue (`#3b82f6`)
- **Inner payload**: smaller rounded rectangle, filled with card color (`#1e293b`)
- **Gap**: transparent at rest; lights up with color during state changes
- **UM mark**: centered in the inner payload, project monospace font

---

## Variant Concept

**Approved direction**: each user or entity may have their own personal-style variant of the Capsule-Pod while maintaining the core structural identity.

### Invariant structure (must be preserved)

All variants must preserve the three-zone anatomy:

1. **Shell** -- outer protective boundary
2. **Gap** -- visible space between shell and payload (integrity layer)
3. **Payload** -- inner data core

### What can vary

- Surface textures and materials (metallic, organic, crystalline, holographic, etc.)
- Shell geometry within the rounded-container family
- Color accent choices beyond the state-mapping colors
- Artistic style (flat, 3D, cinematic, pixel-art, hand-drawn, etc.)
- Environmental context (floating in space, underwater, on a circuit board, etc.)

### What must not vary

- The shell-gap-payload three-zone structure
- The state color mapping (green = verified, red = rejected, amber = expiring)
- The gap-illumination gesture during verification

### Design exploration

Initial variant exploration was generated via Grok's image generation under the Distributed Creatives account. The full variant gallery is available at:
[Grok variant render gallery](https://grok.com/imagine/post/06d18c9d-9316-427b-baa6-115d5a5543a8)

---

## Reference Renders

Cinematic 3D renders are stored in [capsule-pod-reference/](./capsule-pod-reference/).

| File | Description |
|------|-------------|
| `57f9c920-5282-4f24-9cb9-23bdf4cc76fd.jpg` | Cinematic render showing verified (green) and rejected (red) states |
| `grok-video-*.mp4` (7 files) | Animated variant renders exploring different pod styles and materials |
| `Grok link to full list.md` | Source link to the full render gallery |

### Notes for future render iterations

- The color mapping rules from the spec (see table above) should be strictly applied
- Verified state should use `#22c55e` green; rejected state should use `#ef4444` red
- The gap-illumination gesture should be the primary visual differentiator between states
- Background should use the project dark-theme base (`#0f172a`)

---

## Canonical Reference

The full design specification, including all 12 candidate concepts, comparative scoring, and detailed rationale for the Capsule-Pod selection, is in [01-ICONIC-REPRESENTATION.md](../teaching-scripts/01-ICONIC-REPRESENTATION.md).
