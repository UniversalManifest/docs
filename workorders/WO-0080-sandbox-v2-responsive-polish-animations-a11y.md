# WO-0080 -- Responsive Polish, Animations, and Accessibility Audit

**Status:** COMPLETED
**Completed:** 2026-03-01
**Created:** 2026-02-28
**Priority:** P5 (Phase 5 -- Polish + Migration)
**Source:** Sandbox V2 UI Redesign Proposal, Phase 5
**Tags:** [site], [sandbox], [a11y], [css]
**Blocks:** None
**Dependencies:** WO-0077 (scenario detail page rewrite)
**Estimated effort:** 1.5 days
**Proposal:** `.dev/ai/proposals/2026-03-01-02-39-39Z-universalmanifest-sandbox-ui-redesign-proposal.md`

## Objective

Polish the V2 sandbox experience: tune responsive layouts at desktop (1440px), tablet (1024px), and mobile (375px); add session state transition animations and protocol lens message animations; and audit all new components for accessibility (ARIA labels, keyboard navigation, focus management).

## Why this work matters

The V2 components were built for correctness first. This work order adds the polish that makes the experience feel professional and ensures it is accessible to all users, including those using screen readers and keyboard-only navigation.

## Scope

### Files created

- `site/src/styles/sandbox/animations-v2.css` -- Session state transition animations, protocol lens message entrance animations, subject status change animations
- `site/src/styles/sandbox/a11y-v2.css` -- Focus ring styles, high-contrast mode support, reduced-motion media queries

### Files modified

- `site/src/styles/sandbox/responsive-v2.css` -- Tuned breakpoints for tablet and mobile stacking
- All V2 Astro components -- Added ARIA attributes (`role`, `aria-label`, `aria-live`, `aria-expanded`) to interactive elements

### Capabilities delivered

**Responsive:**
- Desktop (1440px+): full 3-column grid layout
- Tablet (1024px): entity columns stack above/below center column
- Mobile (375px): single-column stacked layout

**Animations:**
- Session state badge color transitions (smooth 300ms)
- Protocol lens message entrance (slide-in from source entity direction)
- Subject status indicator transitions
- Respects `prefers-reduced-motion` media query

**Accessibility:**
- All interactive elements have ARIA labels
- HierarchyExplorer tree nodes have `aria-expanded` attributes
- ProtocolLens interactions are in an `aria-live` region for screen reader updates
- Focus management: opening a DetailsCard in JSON mode traps focus appropriately
- Keyboard navigation preserved: arrow keys, space, escape all work in the V2 layout

## Acceptance criteria

- [x] Responsive layout works correctly at 1440px, 1024px, and 375px widths.
- [x] Session state transitions are animated.
- [x] Protocol lens messages animate on entrance.
- [x] `prefers-reduced-motion` is respected (animations disabled).
- [x] All new components have appropriate ARIA attributes.
- [x] Keyboard navigation works throughout the V2 layout.
- [x] No accessibility regressions from V1.
