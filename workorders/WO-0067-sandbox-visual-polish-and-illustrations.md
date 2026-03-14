# WO-0067 -- Sandbox Visual Polish and Illustrations

**Status:** COMPLETED
**Created:** 2026-02-27
**Priority:** HIGH
**Blocks:** None (final polish layer)
**Dependencies:** WO-0063, WO-0064, WO-0065, WO-0066 (all scenarios must exist before polish)
**Estimated effort:** 3-4 days
**Mandate:** [MANDATE-interactive-implementation-sandbox.md](/docs/MANDATE-interactive-implementation-sandbox.md)
**Proposal:** [PROPOSAL-interactive-implementation-sandbox.md](/.dev/ai/proposals/PROPOSAL-interactive-implementation-sandbox.md)

## Objective

Create SVG illustrations for all 25 scenario cards, refine the visual design of the three-panel layout and modal to meet the "beautiful" quality bar, and implement micro-animations for step transitions.

## Why this work matters

The mandate says: "It must be beautiful -- not developer-tool ugly, not demo-day rough." This is the first thing a potential adopter sees. The visual quality must communicate professionalism and production readiness.

## Scope

In scope:
- 25 SVG illustrations for scenario cards (one per scenario)
- Color palette refinement per category
- Step transition animations (panel content fade/slide)
- Lock icon animation for signature verification scenarios
- Progress bar animations for consumer processing
- Bubble entrance/exit animations
- JSON syntax highlighting color scheme refinement
- Dark mode support (inherit from Starlight theme)
- Final responsive design tuning

Out of scope:
- New scenarios (those are complete in WO-0063 through WO-0066)
- Functional changes to the step engine

## Execution tasks

### Phase 1 -- SVG illustrations

- [ ] Design a consistent illustration style (line art, flat color, or the existing animation pipeline style)
- [ ] Create illustrations for Getting Started (4):
  - GS-01: Simple document with checkmark
  - GS-02: Multiple document pieces assembling
  - GS-03: Document with question mark on extra fields
  - GS-04: ID badge resolving to full document
- [ ] Create illustrations for Trust & Verification (5):
  - TV-01: Document with key/lock
  - TV-02: Document with broken seal
  - TV-03: Clock with expired indicator
  - TV-04: Document with missing piece
  - TV-05: Shield rejecting wrong key type
- [ ] Create illustrations for Integration Lanes (8):
  - IL-01: Person silhouette with social links
  - IL-02: Glasses with consent checkmarks
  - IL-03: Two worlds connected by identity
  - IL-04: Spatial grid with anchor pins
  - IL-05: Trust badge with lifecycle timeline
  - IL-06: Blockchain link with credential
  - IL-07: Multiple verification stamps
  - IL-08: Building with display device
- [ ] Create illustrations for Edge Cases (4):
  - EC-01: Timeline with crossed dates
  - EC-02: Unsealed document
  - EC-03: Clock with drift indicator
  - EC-04: Folder with wrong label
- [ ] Create illustrations for Advanced (4):
  - AD-01: One document projecting to three screens
  - AD-02: Document with pointer arrows
  - AD-03: Document with revocation stamp
  - AD-04: Complete verified package

### Phase 2 -- Animations and transitions

- [ ] Step transition: panel content fades out (100ms) and new content fades in (200ms)
- [ ] Bubble entrance: slide up 10px + fade in (200ms ease-out)
- [ ] Bubble exit: fade out (150ms)
- [ ] Lock icon: smooth rotation from open to closed position (TV-01 step 8)
- [ ] Progress bar: smooth width transition (CSS transition)
- [ ] Validation check list: items appear sequentially with 100ms delay between each
- [ ] JSON highlight: colored border fades in when step highlights a field
- [ ] Play mode: slight pulse animation on the step counter during auto-play
- [ ] Create `site/src/styles/sandbox/animations.css` for all animation keyframes

### Phase 3 -- Color and typography refinement

- [ ] Define CSS custom properties per category:
  - `--sandbox-category-getting-started: #3B82F6` (blue)
  - `--sandbox-category-trust: #10B981` (green, with red for failures)
  - `--sandbox-category-integration: #8B5CF6` (purple)
  - `--sandbox-category-edge-cases: #F59E0B` (amber)
  - `--sandbox-category-advanced: #1E40AF` (deep blue)
- [ ] Apply category colors to:
  - Scenario card borders/accents
  - Panel header accent bars
  - Timeline dot colors
  - Bubble border colors
- [ ] Refine JSON syntax highlighting:
  - Keys: `#9333EA` (purple)
  - Strings: `#059669` (green)
  - Numbers: `#2563EB` (blue)
  - Booleans: `#DC2626` (red)
  - Null: `#6B7280` (gray)
  - Brackets: `#374151` (dark gray)
- [ ] Dark mode support: all colors adapt via CSS custom properties / `prefers-color-scheme`

### Phase 4 -- Responsive fine-tuning

- [ ] Test and fix all 25 scenarios at:
  - Desktop (1440px, 1920px)
  - Small desktop (1200px)
  - Tablet (768px, 1024px)
  - Mobile (375px, 414px)
- [ ] Verify modal card grid reflows correctly at all breakpoints
- [ ] Verify three-panel layout transitions correctly at breakpoints
- [ ] Verify bubble positioning is correct at all sizes

## Key file paths (created)

- `site/public/sandbox/illustrations/gs-01.svg` (and 24 more)
- `site/src/styles/sandbox/animations.css`
- Updated: All existing sandbox CSS files with refinements

## Acceptance criteria

- [ ] All 25 scenario cards have unique SVG illustrations
- [ ] Step transitions are smooth and feel polished (no jank)
- [ ] Lock icon animation plays correctly in TV-01
- [ ] Category colors are applied consistently across cards, panels, and bubbles
- [ ] JSON syntax highlighting is readable and attractive
- [ ] Dark mode works without visual issues
- [ ] All scenarios render correctly at desktop, tablet, and mobile widths
- [ ] A non-technical reviewer (CEO) evaluates the sandbox and says it meets the "beautiful" bar
- [ ] `npm run build:clean` succeeds

## Validation commands

- `cd site && npm run build:clean`
- `cd site && npm run dev`
- Manual visual review at multiple viewport sizes
- Manual dark mode review
