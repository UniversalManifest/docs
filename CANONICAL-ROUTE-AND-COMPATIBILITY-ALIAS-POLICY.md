# Canonical Route and Compatibility Alias Policy

This document defines which public routes are canonical, which exist only as compatibility aliases, and which are retirement candidates that must not be treated as long-term authoritative paths.

It exists so future site work can build from one route model instead of preserving sprint-era ambiguity by accident.

## 1. Policy rules

### 1.1 Canonical routes

Canonical routes are the paths that should be linked in current docs, UI, onboarding, and public communications.

Rules:

- New public links should use canonical routes.
- Canonical routes may have compatibility aliases, but aliases must point back to canon rather than becoming parallel entry points.
- Canonical routes should be stable enough that external readers can bookmark them safely.

### 1.2 Compatibility aliases

Compatibility aliases exist to preserve continuity for already-shared URLs, legacy deploys, or shortcut paths.

Rules:

- Aliases may redirect or host thin compatibility wrappers.
- Aliases are allowed to remain public, but they are not the preferred documentation or navigation targets.
- Aliases must not accumulate new information architecture or UI ownership of their own.

### 1.3 Retirement candidates

Retirement candidates are compatibility-only surfaces that should remain available only until documented exit criteria are met.

Rules:

- Do not remove retirement candidates casually.
- Removal requires evidence that canonical replacements exist and that meaningful external dependency on the alias has ended or is acceptably managed.
- Retirement readiness is governed separately by `WO-0188`.

## 2. Canonical route matrix

### 2.1 Standards and public entry routes on `universalmanifest.net`

| Surface family | Canonical route(s) | Compatibility aliases | Notes |
| --- | --- | --- | --- |
| Front door | `/` | none | Consumer-first homepage. |
| Latest public draft | `/spec/latest/` | none | The externally shared public draft path. |
| Curated docs entry | `/docs/` | none | Reader-friendly entry into the broader docs corpus. |
| Reader wrappers | `/about/why-um/`, `/about/one-pager/`, `/use-cases/` | none | Shared-shell explanatory routes. |
| Tool/proof hub | `/learning/` | none | Shared-shell entry to proof and tool surfaces. |
| Sandbox entry | `/sandbox/` | shortcut aliases in `deploy/universalmanifest.net/_redirects` | Scenario aliases remain compatibility shortcuts only. |
| Workbench host | `/workbench/` | `/workbench/index/`, `/workbench/index.html` | The shared-shell host is canonical; index routes are compatibility-only. |
| Proof reading surfaces | `/proof/harness/`, `/proof/journeys/`, `/proof/smoke/` | none | Reading-first proof entry points. |
| Agent-facing entry | `/for-agents/`, `/for-agents/external-agent-onboarding/` | none | Public machine-consumer onboarding. |
| Resolver reference docs | `/reference/resolver-api/` | none | Canonical reader-facing resolver reference. |

### 2.2 Versioned namespace artifacts

| Surface family | Canonical route(s) | Compatibility aliases | Notes |
| --- | --- | --- | --- |
| Versioned artifacts | `/ns/universal-manifest/v0.1/*`, `/ns/universal-manifest/v0.2/*` | none | Versioned artifact URLs are the authoritative published paths. |
| Latest namespace alias | none | `/ns/universal-manifest/latest/*` | Redirect-only alias to a concrete version; never treat `latest/` as authored content. |

### 2.3 Runtime property split

| Property | Canonical route(s) | Compatibility aliases | Notes |
| --- | --- | --- | --- |
| Standards/adoption host | `https://universalmanifest.net/...` | none | Public site, docs, namespace artifacts, discovery files. |
| Runtime resolver host | `https://myum.net/{UMID}`, `https://myum.net/.well-known/myum-resolver.json`, `https://myum.net/openapi.json` | none | Runtime lookup and machine-readable resolver contract. |

## 3. Compatibility-only route classes

These routes may remain published, but they should not be treated as canonical destinations in new content:

- `/workbench/index/`
- `/workbench/index.html`
- `/ns/universal-manifest/latest/*`
- sandbox shortcut routes in `deploy/universalmanifest.net/_redirects`
- legacy namespace/property paths served through `localartist.network`

The rule for all of them is the same: preserve continuity, but keep the current public narrative, navigation, and authored docs pointed at the canonical route.

## 4. Current retirement candidates

These are compatibility layers or legacy surfaces that should be considered retirement candidates rather than permanent architecture:

- `/workbench/index/`
- `/workbench/index.html`
- `deploy/localartist.network/`
- alias-only sandbox shortcut routes once evidence shows they are no longer valuable

These are not approved for removal by this document. This document only classifies them so `WO-0188` can later define retirement readiness and sequencing.

## 5. Route-authoring rules for future work

Use these rules when adding or revising public routes:

1. Add new public narrative links only to canonical routes.
2. If a compatibility alias is needed, document why it exists and what canonical route it points to.
3. Do not widen the primary public menu beyond `Home` and `Latest Spec` without a new explicit decision.
4. Keep `universalmanifest.net` focused on standards, adoption, tools, and discovery; keep `myum.net` focused on resolution/runtime.
5. Keep versioned artifact paths immutable; changes go to new versions, not edits in place.
6. Keep `latest/` aliases as redirects, not mutable content targets.
7. If a route is only kept for continuity, say so explicitly in docs or deploy guidance rather than implying it is first-class.

## 6. Deployment implications

Deploy guidance should reflect this policy:

- edge redirects should preserve compatibility aliases but point to canonical destinations
- static-host configs should not introduce new parallel public entry points casually
- deploys should preserve the property split between `universalmanifest.net` and `myum.net`
- legacy `localartist.network` hosting should be treated as compatibility infrastructure only

## 7. Related documents

- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
- `docs/reports/2026-04-13-post-wo-0179-surface-disposition-and-unification-strategy.md`
- `docs/workorders/WO-0183-canonical-route-and-compatibility-alias-policy.md`
- `docs/workorders/WO-0188-compatibility-surface-retirement-readiness.md`
