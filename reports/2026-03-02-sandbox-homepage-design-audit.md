# Sandbox Homepage Design Audit (Choose a Scenario)

Date: 2026-03-02
Scope: `/sandbox/` landing page visual/UX audit against the docs homepage (`/`) and sandbox scenario detail pages (`/sandbox/<scenario>/`).

## What I audited

Pages reviewed:
- `http://127.0.0.1:4300/sandbox/` (problem page)
- `http://127.0.0.1:4300/` (site homepage baseline)
- `http://127.0.0.1:4300/sandbox/gs-01-first-manifest-v2/` (scenario detail baseline)

Code reviewed:
- `site/src/pages/sandbox/index.astro`
- `site/src/components/sandbox/ScenarioModal.astro`
- `site/src/components/sandbox/ScenarioCard.astro`
- `site/src/styles/sandbox/modal.css`
- `site/src/styles/sandbox/layout-v3.css`
- `site/src/pages/sandbox/[...scenario].astro`

Evidence screenshots:
- `.dev/ai/reports/sandbox-home-audit-chooser-before.png`
- `.dev/ai/reports/sandbox-home-audit-site-home.png`
- `.dev/ai/reports/sandbox-home-audit-scenario-detail-intro.png`
- `.dev/ai/reports/sandbox-home-audit-scenario-detail-running.png`

## Executive summary

Your read is correct: the chooser page currently feels like an older isolated tool screen, while the rest of the site and V2 scenario pages feel like a modern product surface. The mismatch is structural (layout shell and tokens), not just “styling polish.”

The page also has a heavy information overload problem (56 cards visible by default data set, many duplicate V1/V2 families), which makes it feel noisy and low-quality even when the underlying scenario content is strong.

## Key findings

### 1) Structural shell mismatch (major)

The chooser page is built as a standalone full document and does not use the broader docs shell or the richer sandbox V3 framing.

Evidence:
- `site/src/pages/sandbox/index.astro:24-33` renders a bare `<!doctype html>` page with `<ScenarioModal />` directly in `<body>`.
- No shared site header/navigation/breadcrumb is rendered on this page.

Why this hurts design quality:
- It visually disconnects `/sandbox/` from the rest of `universalmanifest.net`.
- Users lose orientation/context compared with the homepage and scenario detail pages.

### 2) Token/typography mismatch vs V2/V3 sandbox pages (major)

Chooser uses older dark token set and system font; scenario detail V3 uses a light token system with intentional typography.

Evidence:
- Chooser token source: `site/src/styles/sandbox/modal.css:3-8` (`--sb-*`, dark background, system-ui font).
- Scenario detail V3 token source: `site/src/styles/sandbox/layout-v3.css:7-24` (light tokens, `Inter`, `JetBrains Mono`).
- Scenario detail imports full V2+V3 style stack: `site/src/pages/sandbox/[...scenario].astro:736-754`.

Why this hurts design quality:
- The same “sandbox product” appears to have two unrelated design systems.
- Transition from chooser to scenario feels like a context jump, not one coherent experience.

### 3) Information architecture overload and duplication (major)

Current chooser exposes too many cards at once and mixes legacy + V2 in one grid without clear hierarchy.

Measured evidence (from rendered HTML):
- Total cards: 56
- Unique normalized scenario families: 34
- Duplicate families (V1 + V2 shown together): 22

Why this hurts design quality:
- It reads as cluttered and hard to scan.
- Users are forced to decode “which one should I use” instead of being guided.

### 4) Illustration inconsistency (major visual regression)

A large portion of cards render fallback icons instead of scenario illustrations, especially V2 items.

Measured evidence:
- Cards with image: 25
- Cards without image: 31
- V2 cards without image: 25 of 25

Root cause in code:
- `site/src/components/sandbox/ScenarioCard.astro:43-69` illustration map includes only V1 IDs.
- V2 IDs (e.g., `*-v2`) are not mapped, so they always fall back to generic icon (`:89-97`).

Why this hurts design quality:
- Grid appears partially unfinished.
- The visual rhythm breaks because image-backed and icon fallback cards mix unpredictably.

### 5) Card readability and density issues (moderate)

Cards are optimized for compact density, not legibility.

Evidence:
- Fixed 3-column dense grid: `site/src/styles/sandbox/modal.css:124-128`.
- Title forced to single-line ellipsis: `:232-240`.
- Description clamped to 2 lines: `:242-250`.

Why this hurts design quality:
- Long scenario names lose meaning.
- Description truncation plus dense layout makes many cards visually similar.

### 6) Legacy interaction model (moderate)

Chooser relies on plain search/filter and “show more” without a clear primary journey.

Evidence:
- Toolbar-only controls in `ScenarioModal.astro:51-70`.
- Collapsed sections by category in `ScenarioModal.astro:72-105`.

Why this hurts design quality:
- Users get a database-like picker instead of a curated, narrative landing flow.
- The page does not echo the high-quality onboarding behavior used by V3 scenario intro overlays.

### 7) Intermittent dev instability observed (minor, but relevant)

During audit, one existing dev-server process briefly returned HTTP 500 for `/sandbox/` before recovering. A fresh Astro process served it normally.

Interpretation:
- Likely hot-state/HMR instability, not a persistent route failure.
- Still worth tracking separately because it can mask UX issues during development review.

## Why it currently looks bad

In one line: it combines an outdated visual system, overloaded content, and inconsistent asset coverage in a route that lacks the site’s framing and narrative guidance.

Concretely:
- Old tokens + old density rules
- Too many cards and duplicate options at once
- Missing illustrations for all V2 cards
- No strong “start here” hierarchy
- Visual language mismatch with both homepage and scenario detail pages

## Design direction to make it fit the rest of the site

### Target experience

`/sandbox/` should feel like the front door to the same V3 sandbox product, not a separate utility screen.

### Proposed changes

1. Adopt V3 visual language on chooser
- Reuse V3 tokens and typography (`layout-v3.css`) for the chooser surface.
- Introduce a light, card-based hero and section framing matching scenario intro aesthetics.

2. Introduce clear guidance hierarchy
- Add a hero with: title, concise explainer, and recommended entry scenarios.
- Add a clear default path: “Start with V2 scenarios.”

3. Deduplicate by default
- Show one card per scenario family by default (prefer V2 where available).
- Move legacy V1 to a secondary toggle or separate section (“Legacy V1 Scenarios”).

4. Fix illustration coverage
- Expand illustration mapping logic so V2 cards inherit V1 illustration assets where applicable.
- Ensure all default-visible cards have deliberate visual treatments.

5. Improve card readability
- Increase card breathing room and text hierarchy.
- Remove forced single-line title truncation for desktop where space allows.
- Keep concise metadata but lower visual noise.

6. Align navigation framing
- Provide stronger orientation controls (back to docs context + clear sandbox purpose block).
- Keep sandbox custom experience, but make it visually/behaviorally coherent with site standards.

## Implementation plan (how I’ll make it fit)

Phase 1: Data shaping and content hierarchy
- Update `site/src/pages/sandbox/index.astro` to build a presentation model that:
  - collapses duplicate families
  - prefers V2 as primary
  - optionally exposes V1 in a secondary mode

Phase 2: Component redesign
- Refactor `site/src/components/sandbox/ScenarioModal.astro` into a V3-style landing composition:
  - hero section
  - featured quick-start row
  - categorized cards with cleaner grouping

Phase 3: Card system update
- Update `site/src/components/sandbox/ScenarioCard.astro`:
  - normalize illustration resolution for V2 IDs
  - improve title/description rendering and metadata hierarchy

Phase 4: Styling unification
- Replace/augment `site/src/styles/sandbox/modal.css` with a V3-aligned stylesheet that references shared V3 tokens from `site/src/styles/sandbox/layout-v3.css`.

Phase 5: Verification
- Validate desktop and mobile layouts.
- Verify all default-visible cards have expected visual assets.
- Verify filter/search/toggle behaviors remain correct after dedupe and hierarchy changes.

## Success criteria

- Chooser looks like the same design family as V3 scenario pages.
- Users can identify a recommended starting scenario within seconds.
- Duplicate V1/V2 confusion is removed from default view.
- Illustration consistency is restored for primary cards.
- Route maintains functional parity (search/filter/navigation) with improved readability.

## Recommendation

Proceed with a focused redesign pass on `/sandbox/` before adding any new scenario content to the landing page. The current issue is primarily IA and design-system coherence, not missing functionality.
