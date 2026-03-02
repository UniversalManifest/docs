# WO-0074 -- SubjectPanel: Exchanged Object Display with Dual-Mode

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P2 (Phase 2 -- Panels)
**Source:** Sandbox V2 UI Redesign Proposal, Task T6
**Tags:** [site], [sandbox], [component]
**Blocks:** WO-0075
**Dependencies:** WO-0070 (DetailsCard)
**Estimated effort:** 1 day
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Build the SubjectPanel component that occupies the lower portion of the center column in the V2 layout. It displays the object being exchanged or resolved between the two entities (a manifest shard, a DID document, a credential, etc.) using a DetailsCard with dual-mode rendering (hierarchy/JSON).

## Why this work matters

The V1 sandbox had no concept of a "subject" -- the thing being exchanged between entities. The object was implicitly buried in step annotations. The SubjectPanel gives the exchanged object a dedicated display area, making it clear what is being passed between parties during a protocol interaction.

## Scope

### Files created

- `site/src/components/sandbox/SubjectPanel.astro` -- Astro shell for subject display
- `site/src/scripts/sandbox/subject-panel.ts` -- Client-side logic: subject data binding, status updates, DetailsCard wiring
- `site/src/styles/sandbox/subject.css` -- Subject panel styles with `--sb-subject-accent` color

### Capabilities

- Displays the subject type label (e.g., "manifest-shard", "did-document", "credential")
- Shows subject data in a DetailsCard with dual-mode (hierarchy/JSON)
- Subject status indicator (idle, in-transit, resolved, rejected)
- Updates per step as the protocol progresses
- Uses `--sb-subject-accent` (orange) for visual differentiation
- Uses BEM naming with `sb-sp-` prefix

## Acceptance criteria

- [x] SubjectPanel renders subject type label and data in a DetailsCard.
- [x] JSON toggle works for the subject DetailsCard.
- [x] Subject status updates as the scenario progresses.
- [x] Visual differentiation from entity panels via accent color.
