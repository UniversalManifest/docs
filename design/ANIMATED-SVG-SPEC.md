# Animated SVG Technical Specification for Universal Manifest

## Purpose

Define hard technical constraints for animated SVG explainers used in Universal Manifest docs.

## 1. Output format requirements

- Standalone valid SVG 1.1/2.0 markup.
- No external scripts.
- No remote dependencies.
- Include `<title>` and `<desc>`.
- Include explicit `viewBox` and responsive sizing strategy.

## 2. Accessibility requirements

- Provide meaningful `<title>` and `<desc>` that summarize the learning objective.
- Preserve clear visual order matching conceptual order.
- Ensure text contrast ratio >= 4.5:1.
- Provide reduced-motion behavior:
  - `@media (prefers-reduced-motion: reduce)`
  - stop non-essential movement
  - keep static informative frame

## 3. Motion requirements

- Motion must explain sequence or causality.
- Decorative-only motion is prohibited.
- Use deterministic timing with explicit durations.
- Include loop-safe start/end continuity.
- Avoid jitter and rapid flashing.

## 4. Performance budgets

- Hero SVG target: <= 180 KB.
- Inline SVG target: <= 220 KB.
- Full-page tutorial target: <= 320 KB.
- Avoid expensive blur/filter stacks.
- Keep concurrent animation tracks minimal.

## 5. Content fidelity requirements

Animation text and labels must align with UM terminology:

- `@id (UMID)`
- `subject`
- `issuedAt` / `expiresAt`
- `claims`
- `consents`
- `pointers`
- `shards`
- resolver
- verifier

Do not introduce claims that contradict:

- `spec/v0.1/schema.json`
- `spec/v0.2/schema.json`
- `docs/DECISIONS.md`

## 6. Cross-device behavior

- Must render clearly on desktop and mobile widths.
- Must not cause large layout shift on page load.
- Must remain legible at 320px width and 2x pixel density.

## 7. Integration requirements

- Place assets under `site/public/animations/`.
- Refer to assets using root-relative URLs in docs pages.
- If animation fails to render, page must still be understandable from text + static fallback image.

## 8. Verification requirements

Before acceptance, confirm:

1. `cd site && npm run build` passes.
2. Reduced-motion fallback works in browser emulation.
3. SVG output meets file-size budget.
4. Labels and sequence match source-grounded narrative.

