# 2026-04-13 Post-WO-0179 Surface Disposition and Unification Strategy

## Purpose

This report turns the comprehensive project/property/surface map into an actionable structural strategy.

It answers three questions:

1. Which surface families are already unified?
2. Which surfaces should remain as they are?
3. Which surfaces should be merged, aliased, or retired in the next architectural wave?

This is a planning and governance output, not an implementation report.

## 1. Current Surface Classification

### 1.1 Already unified under the new shared shell family

These routes now present a coherent public/tool-shell language:

- `/`
- `/docs/`
- `/about/why-um/`
- `/about/one-pager/`
- `/use-cases/`
- `/learning/`
- `/sandbox/`
- `/workbench/`
- `/review/*`

Ownership:

- `site/src/layouts/PublicSurfaceLayout.astro`
- `site/src/layouts/ToolSurfaceLayout.astro`
- `site/src/components/ui/`

### 1.2 Still Starlight-owned by design

These remain content-first reading surfaces whose source of truth is the Starlight content tree:

- `about/`
- `conformance/`
- `getting-started/`
- `governance/`
- `guides/`
- `handouts/`
- `implementations/`
- `integrations/`
- `proof/`
- `publishing/`
- `reference/`
- `spec/`
- `use-cases/`
- `for-agents.md`
- `external-agent-onboarding.md`
- `index.md`

This is not automatically a problem. The key decision is that Starlight remains the content authoring system until there is a strong reason to migrate a family into fully custom Astro pages.

### 1.3 Fragmented or legacy surfaces

These are the clearest remaining sprint-era fragments:

- `/spec/latest/` still injects checked-in HTML from `docs/W3C-STYLE-SPEC.html`
- `/workbench/` is unified at the route level, but the app still lives as a subordinate static payload
- `/workbench/index/` remains an alias-only compatibility shim
- `/harness/index.html` remains a raw static app
- `site/public/resolver/index.html`, `ops.html`, and `result.html` remain legacy static UI surfaces
- `/tools/concept-explorer/` remains a raw static surface
- `site/src/pages/404.astro` is still standalone and outside the newer shell logic

## 2. Surface Disposition Matrix

### 2.1 Keep as canonical

These surfaces are structurally correct and should remain authoritative:

- `services/myum-resolver/`
- `deploy/universalmanifest.net/`
- published namespace artifacts under `/ns/universal-manifest/...`
- machine-readable discovery files:
  - `/.well-known/universal-manifest.json`
  - `/.well-known/security.txt`
  - `/llms.txt`
  - `/agent/fixture-catalog.json`
  - `/agent/sandbox-scenarios.json`
- `site/public/harness/index.html` as the raw harness payload
- `site/public/workbench/app/index.html` and `site/public/workbench/workbench.js` as the raw workbench payload
- evidence assets under:
  - `site/public/animations/`
  - `site/public/diagrams/`
  - `site/public/sandbox/illustrations/`

### 2.2 Keep, but only as alias or compatibility layer

- `site/public/workbench/index.html`
  - keep as redirect-only
- `site/src/pages/workbench/index/index.astro`
  - keep as alias-only while external links still exist
- `deploy/localartist.network/`
  - compatibility layer only; do not treat as active canonical property

### 2.3 Merge or re-home over time

- `site/public/harness/fixtures/*`
- `site/public/sandbox/fixtures/*`

Decision:

- authored source of truth should live in `examples/`
- published copies can remain as generated mirrors for browser tools

- `site/public/resolver/ops.html`
- `site/public/resolver/result.html`

Decision:

- either fold into `site/public/resolver/index.html`
- or retire if no longer operationally useful

- animation and diagram naming families

Decision:

- keep the assets
- normalize naming conventions over time
- maintain aliases only where public links require continuity

### 2.4 Retire candidates

These are not immediate removals, but they are the cleanest future retirement candidates:

- `/workbench/index/` after compatibility demand is gone
- standalone resolver auxiliary pages if their workflows are absorbed elsewhere
- legacy `localartist.network` deployment material once compatibility requirements truly end

## 3. Recommended Next Architectural Sequence

This is the recommended order for the next execution wave after the planning lane.

### Sequence 1: Finish classification and path policy

Do first:

- decide which public routes are canonical
- decide which are compatibility aliases
- decide which are retirement targets

This avoids accidental parallel redesign of routes that should not survive long-term anyway.

### Sequence 2: Normalize remaining static tool surfaces

Target surfaces:

- raw harness entry behavior
- resolver static pages
- concept explorer static page
- 404 page shell alignment

Goal:

- make the remaining non-Starlight public surfaces feel related at the route and framing level
- do not rewrite internals unless route-level framing and ownership are already stable

### Sequence 3: Decide the long-term fate of `/spec/latest/`

This is the most important remaining legacy fragment.

Decision surface:

- keep the W3C-style injected HTML model permanently
- or progressively wrap/rebuild more of it under a stronger shared-shell pattern without losing standards-reader expectations

### Sequence 4: Keep Starlight-owned content families content-first

Do not migrate large content families out of Starlight without a very strong reason.

Current recommendation:

- keep Starlight as the authoring system for the markdown corpus
- selectively re-present high-value entry routes through shared-shell wrappers where user experience requires it

## 4. Clear Calls

### 4.1 What should not be touched casually

- `services/myum-resolver/`
- published namespace artifacts
- discovery files
- raw harness/workbench payloads unless there is a bounded migration plan

### 4.2 What is safe to unify next

- resolver static pages
- concept explorer framing
- 404 route presentation
- alias and redirect policy documentation

### 4.3 What should be treated as generated mirrors

- published fixture copies under `site/public/harness/fixtures/`
- published fixture copies under `site/public/sandbox/fixtures/`

Authored fixture truth should remain in the example corpus, not in multiple public mirrors.

## 5. Outcome

The project is no longer in the phase of “what exists?” The deeper question is now “which surfaces are canonical, which are compatibility layers, and which should be retired over time?”

This report establishes that answer at the architectural level:

- the public/tool shell family is substantially real now
- the docs corpus can remain Starlight-owned
- the runtime boundary is already structurally clean
- the remaining fragmentation is concentrated in a small set of legacy/static tool surfaces and compatibility aliases

That is the correct starting point for any future unification wave.
