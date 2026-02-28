# Teaching Scripts

Short animated explainers that illustrate Universal Manifest concepts using a consistent visual character -- the Capsule-Pod.

---

## What This Directory Is For

This directory contains the design system, format specification, and script library for producing teaching animations about Universal Manifest. These are not technical diagrams or spec walkthroughs. They are **stories** -- a small character (the UM Capsule-Pod) travels between systems, gets verified, opens up to reveal its contents, and helps the viewer understand what portable, verifiable state looks like in practice.

The goal: a viewer watches a 30-second animation and thinks "oh, I get what this does" without ever seeing a line of JSON.

---

## Directory Structure

```
docs/teaching-scripts/
  README.md                         -- This file
  01-ICONIC-REPRESENTATION.md       -- The visual identity: what the UM "character" looks like
  02-SCRIPT-FORMAT.md               -- The standard format for writing teaching scripts
  03-SCRIPT-IDEAS.md                -- 20 script concepts organized by difficulty
  scripts/                          -- (future) Individual script files (TS-001-*.md, etc.)
```

---

## Staged Approach

### Stage 1: Iconic Representation (DONE)
Define the visual character -- the Capsule-Pod -- and the supporting visual vocabulary (shield overlay for verification, prism for projection). This is the foundation everything else builds on.

### Stage 2: Script Format (DONE)
Define the scene-by-scene format that scripts follow. This ensures consistency across all scripts and gives animators a predictable blueprint to work from.

### Stage 3: Script Ideas (DONE)
Brainstorm and organize 20 teaching script concepts across five categories, from beginner introductions to advanced integration lane scenarios.

### Stage 4: Script Production (NEXT)
Write full scene-by-scene scripts for the highest-priority concepts. Each script goes in `scripts/TS-NNN-slug.md` following the format from Stage 2.

### Stage 5: Animation Production (FUTURE)
Convert approved scripts into actual SVG animations, matching the visual style of the existing animations in `site/public/animations/`. These use the project's established dark theme, card-based layout, and CSS animation approach.

### Stage 6: Sandbox Integration (FUTURE)
Integrate teaching animations into the interactive sandbox (see the CEO mandate in `docs/MANDATE-interactive-implementation-sandbox.md`). Teaching scripts become the narrative layer on top of the sandbox's interactive step-through system.

---

## How to Add a New Script

1. **Read the format**: Review `02-SCRIPT-FORMAT.md` for the required structure.
2. **Pick a concept**: Check `03-SCRIPT-IDEAS.md` for existing ideas, or propose a new one.
3. **Assign an ID**: Use the next available `TS-NNN` number.
4. **Write the script**: Create `scripts/TS-NNN-slug.md` with the full metadata block and scene breakdown.
5. **Check the checklist**: The format doc includes a submission checklist at the bottom.
6. **Add to the ideas doc**: If this is a new concept not already in `03-SCRIPT-IDEAS.md`, add a summary entry.

---

## Relationship to Existing Assets

### SVG Animations (`site/public/animations/`)
The existing SVG animations in the site are technical explainer diagrams -- they show the object model, the core flow, integration lanes, and workbench lifecycle. Teaching scripts are a **complementary layer** that tells the same stories in a more narrative, character-driven way. The two can coexist: the existing animations serve as reference diagrams, while teaching scripts serve as introductory explainers.

Teaching script animations should use the same visual palette (dark theme with `#0f172a` background, `#1e293b` cards, blue/green/amber/violet accents) and typography (system-ui font stack, monospace for code) to maintain visual consistency across the site.

### Interactive Sandbox (WO-0060+)
The sandbox mandate calls for an interactive step-through experience where users can see the spec in action. Teaching scripts provide the **narrative scaffolding** for those step-throughs. Each teaching script's scenes can map directly to sandbox steps: Scene 1 = Step 1 in the sandbox, and so on. The sandbox adds interactivity (modify values, see outcomes change); the teaching script provides the story and pacing.

### Conformance Suite and Reference Implementation
The sandbox uses real validation logic from `packages/universal-manifest/`. Teaching scripts abstract away that implementation detail -- they show what verification *looks like* (the pod glowing green) rather than what it *does* (JCS canonicalization + Ed25519 signature check). The two layers complement each other: the teaching script builds intuition, the sandbox provides proof.

---

## Design Philosophy

**Pixar, not PowerPoint.** The pod is a character with visual personality. It glows, it travels, it gets inspected, it opens up. It is not a rectangle on a flowchart.

**One idea, one script.** Each script teaches exactly one concept. Complexity comes from watching multiple scripts in sequence, not from cramming everything into one.

**Show, then name.** The visual metaphor comes first (the gap lights up green), the label comes second ("that means the signature is valid"). Never lecture before demonstrating.

**Abstract the spec.** A viewer should understand what Universal Manifest does without knowing that it uses JSON-LD, Ed25519, or JCS. Those details are for the spec and the sandbox. The teaching scripts are for intuition.
