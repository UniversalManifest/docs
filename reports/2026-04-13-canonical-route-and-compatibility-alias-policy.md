# 2026-04-13 Canonical Route and Compatibility Alias Policy

## Purpose

This report closes `WO-0183` by turning the earlier surface-classification work into one authoritative route policy.

The project had already identified canonical, alias-only, and retirement-candidate surfaces in analysis form. What was missing was a single policy artifact that future implementation work could cite directly.

## What changed

### 1. Added a canonical route policy

Created:

- `docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md`

That document now defines:

- what counts as a canonical route
- what counts as a compatibility alias
- what counts as a retirement candidate
- the current canonical route matrix for:
  - public entry routes
  - namespace artifact routes
  - the `universalmanifest.net` versus `myum.net` split

### 2. Clarified compatibility-only classes

The route policy explicitly classifies these as compatibility-only rather than first-class canonical surfaces:

- `/workbench/index/`
- `/workbench/index.html`
- `/ns/universal-manifest/latest/*`
- sandbox shortcut aliases in `deploy/universalmanifest.net/_redirects`
- `localartist.network` namespace/property hosting

### 3. Updated architecture and deploy guidance

Updated:

- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
- `deploy/universalmanifest.net/README.md`
- `deploy/universalmanifest.net/CLOUDFLARE-PAGES.md`

These now point to the route policy so deploy and architecture guidance stop treating route posture as implicit tribal knowledge.

## Result

Future work no longer needs to infer the route model from scattered reports and code.

The authoritative posture is now:

- canonical public links should point at the calm front door, latest spec, and the current shared-shell surfaces
- compatibility aliases may remain public, but they should not accumulate new IA ownership
- retirement-candidate routes remain live only until `WO-0188` defines and verifies safe removal criteria

## Verification

Manual verification completed:

- the new policy aligns with the current route model documented in `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
- the policy aligns with the post-`WO-0179` surface strategy report
- deploy docs now reference the policy instead of leaving alias behavior implicit

No public route behavior was changed in this work order. This is a governance-and-deploy-guidance closure, not a routing implementation change.
