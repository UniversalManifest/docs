# Animation Placement Plan

## Objective

Map animated SVG explainers to high-impact pages that improve first-read comprehension and implementation readiness.

## Placement map

## 1) Overview hero

- Page: `site/src/content/docs/index.md`
- Asset: `site/public/animations/um-core-flow-pilot.svg`
- Purpose: Explain UM core envelope and resolve/validate/consume path in one glance.
- Placement: top of page after first framing paragraph.
- Status: **integrated** (WO-0042 upgraded to production dark theme)

## 2) First-time overview page

- Page: `site/src/content/docs/getting-started/universal-manifest-overview.md`
- Asset: `site/public/animations/um-overlay-lanes-pilot.svg`
- Purpose: Show how overlay lanes connect to one shared UM envelope.
- Placement: after "High-level flow" content.
- Status: **integrated** (WO-0042 upgraded to production dark theme)

## 3) System overview diagram

- Page: `site/public/diagrams/universal-manifest-overview-template.svg`
- Purpose: Complete system architecture Issuance/Distribution/Consumption.
- Status: **integrated** (WO-0042 upgraded to animated dark theme)

## 4) Workbench page

- Page: `site/src/content/docs/getting-started/workbench.md`
- Asset: `site/public/animations/scenario-07-workbench-explainer.svg`
- Scenario: Editor lifecycle (import -> edit -> validate -> export).
- Status: **integrated** (WO-0043 upgraded to production dark theme)

## 5) Harness page

- Page: `site/src/content/docs/proof/harness.md`
- Asset: `site/public/animations/scenario-08-harness-explainer.svg`
- Scenario: Fixture load -> quick checks -> resolver probe -> evidence capture.
- Status: **integrated** (WO-0043 upgraded to production dark theme)

## 6) Integration lane pages

All integration lane pages have embedded SVG explainers upgraded to production dark theme (WO-0043):

| Page | Asset | Status |
|------|-------|--------|
| `integrations/social.md` | `scenario-09-social-integration.svg` | **integrated** |
| `integrations/proof-of-personhood.md` | `scenario-10-pop-integration.svg` | **integrated** |
| `integrations/oma-trust.md` | `scenario-11-omatrust-integration.svg` | **integrated** |
| `integrations/rp1-spatial-fabric.md` | `scenario-12-rp1-integration.svg` | **integrated** |
| `integrations/smart-glasses.md` | `scenario-13-smart-glasses-integration.svg` | **integrated** |
| `integrations/metaverse.md` | `scenario-14-metaverse-integration.svg` | **integrated** |
| `integrations/chia-vc.md` | `scenario-15-chia-vc-integration.svg` | **integrated** |

## 7) Scenario animations (WO-0042)

| Asset | Purpose | Status |
|-------|---------|--------|
| `scenario-01-object-model.svg` | Manifest structure breakdown | **created** |
| `scenario-03-consent-policy-flow.svg` | Consent toggle gating flow | **created** |
| `scenario-04-user-journey-sequence.svg` | End-to-end user flow | **created** |
| `scenario-06-motion-tutorial.svg` | Visual objects and icons tutorial | **created** |

## Selection rationale

- Prioritize first-read pages first (`/` and getting-started overview).
- Keep pilots close to pages already carrying onboarding narrative.
- All tool and integration lane pages now have contextual explainers.
- Production dark theme (#0f172a background) applied consistently across all assets.
