# Universal Manifest — Comprehensive Project, Property, and Surface Map

This document is the deepest single-file orientation map for Universal Manifest.

It exists to answer five questions clearly:

1. What the project is.
2. Which public properties exist.
3. Which surfaces belong to each property.
4. Which repo areas own those surfaces.
5. Which documents are the source of truth for each layer.

If `README.md` is the short front door and `STATE-OF-THE-PROJECT.md` is the current snapshot, this file is the full structural map.

Route posture for canonical versus compatibility-only public paths is defined separately in:

- `docs/CANONICAL-ROUTE-AND-COMPATIBILITY-ALIAS-POLICY.md`

## 1. Executive Model

Universal Manifest is not a single app and not only a specification.

It is a multi-surface standards program with five coordinated layers:

1. **Normative standard layer**
   - versioned spec artifacts, schemas, contexts, conformance rules
2. **Fixture and proof layer**
   - examples, invalid fixtures, standalone conformance material, journeys, smoke checks
3. **Public adoption layer**
   - homepage, docs, explainers, use-case pages, guides, governance pages
4. **Interactive tool layer**
   - sandbox, workbench, harness, concept explorer, browser-visible proof surfaces
5. **Runtime layer**
   - resolver contract and live UMID lookup on `myum.net`

The project is therefore half standard, half proof system, and half public adoption program. That complexity is intentional: the goal is to prove the format is understandable, implementable, and deployable.

## 2. Public Properties

The project operates across two public internet properties and one internal documentation mirror.

### 2.1 `universalmanifest.net`

Role:

- standards host
- public learning and adoption host
- docs and governance host
- public proof/tool entry host
- machine-readable discovery host
- namespace artifact host

This property is the public face of the project.

It now follows a calm-front-door model:

- `/` is the consumer-first homepage
- `/spec/latest/` is the latest W3C-style draft specification
- richer reading, proof, and tool surfaces sit behind that front door

### 2.2 `myum.net`

Role:

- UMID resolver host
- runtime contract host
- machine-readable runtime discovery host

This property is deliberately separate from the standards property.

The split exists so the public standard is not confused with a specific runtime service, while still proving the runtime contract can exist in production.

### 2.3 NotebookLM mirror

Repo path:

- `notebooklm-knowledge-vault/`

Role:

- mirrored knowledge surface derived from canonical docs/spec state

This is not the source of truth. It is a derivative memory surface for retrieval and onboarding workflows.

## 3. Repo Ownership Map

These are the major top-level repo areas and what they own.

| Area | Role | Owns |
| --- | --- | --- |
| `spec/` | Normative contract | versioned spec text, contexts, schemas, conformance definitions |
| `examples/` | Fixture and example corpus | valid, invalid, and near-real example manifests plus runnable examples |
| `conformance/` | Language-neutral validation packaging | standalone suite material and adapters |
| `packages/universal-manifest/` | TypeScript reference helper | validation, verification, scripts, journey and smoke runners |
| `services/myum-resolver/` | Runtime resolver | `myum.net` contract and implementation |
| `site/` | Public web property | homepage, docs shell, public routes, review pages, shared UI, static tools |
| `docs/` | Canonical project memory | status, decisions, architecture, work orders, reports, journeys, governance |
| `integrations/` | Integration-lane source material | adopter/domain notes used across the public docs corpus |
| `deploy/` | Deployment baselines | hosting configs and property-specific deployment artifacts |
| `research/` | Imported context | external research and source material |
| `adopters/` | Adoption-facing records | adopter registry and related metadata |
| `notebooklm-knowledge-vault/` | Derived mirror | mirrored docs/spec knowledge surface |

## 4. Canonical Source of Truth by Layer

This is the most important “where do I trust the answer?” map.

### 4.1 Standard and contract truth

Primary sources:

- `spec/v0.1/`
- `spec/v0.2/`
- `examples/v0.1/`
- `examples/v0.2/`
- `conformance/`

Use when the question is:

- What is the contract?
- What is required?
- What counts as valid or invalid?
- What changed between versions?

### 4.2 Public site and route truth

Primary source:

- `site/`

Sub-ownership:

- `site/src/pages/` for Astro route entrypoints
- `site/src/content/docs/` for Starlight docs content families
- `site/public/` for static assets, machine-readable files, harness/workbench payloads, diagrams, animations
- `site/src/components/` and `site/src/layouts/` for shared shell/UI ownership

### 4.3 Runtime truth

Primary source:

- `services/myum-resolver/`

Use when the question is:

- How does UMID resolution work?
- Which runtime endpoints exist?
- What headers, cache policy, or redirect behavior are expected?

### 4.4 Governance and program-memory truth

Primary source:

- `docs/`

Key files:

- `docs/STATE-OF-THE-PROJECT.md`
- `docs/CRITICAL-PATH.md`
- `docs/DECISIONS.md`
- `docs/workorders/WO-INDEX.md`
- `docs/reports/`

Use when the question is:

- Why was a decision made?
- What work is complete?
- What evidence exists?
- How do the properties and surfaces fit together strategically?

### 4.5 Derived mirror truth

Derived-only surface:

- `notebooklm-knowledge-vault/`

Use for retrieval convenience, not for authoritative editing decisions.

## 5. `universalmanifest.net` Surface Map

This section maps the public standards/adoption property by surface family.

### 5.1 Front-door and reader surfaces

| Public route family | Purpose | Source of truth |
| --- | --- | --- |
| `/` | consumer-first homepage | `site/src/pages/index.astro` |
| `/spec/latest/` | latest W3C-style draft spec | `site/src/pages/spec/latest.astro` + `docs/W3C-STYLE-SPEC.html` |
| `/docs/` | curated docs entry | `site/src/pages/docs/index.astro` |
| `/docs/overview/` | long-form docs overview | `site/src/content/docs/index.md` |
| `/about/why-um/` | plain-language explanation | `site/src/pages/about/why-um.astro` |
| `/about/one-pager/` | short reader handoff | `site/src/pages/about/one-pager.astro` |
| `/use-cases/` | audience/use-case routing | `site/src/pages/use-cases/index.astro` |

### 5.2 Tool and proof entry surfaces

| Public route family | Purpose | Source of truth |
| --- | --- | --- |
| `/learning/` | shared hub for tools and proof surfaces | `site/src/pages/learning/index.astro` |
| `/sandbox/` | sandbox chooser under shared shell | `site/src/pages/sandbox/index.astro` |
| `/sandbox/...` | individual scenario routes | `site/src/pages/sandbox/[...scenario].astro` |
| `/workbench/` | shared-shell workbench host route | `site/src/pages/workbench/index.astro` |
| `/workbench/app/` | preserved raw workbench payload | `site/public/workbench/app/index.html` |
| `/workbench/index.html` | compatibility redirect to payload | `site/public/workbench/index.html` |
| `/harness/index.html` | raw harness app | `site/public/harness/index.html` |
| `/proof/harness/` | harness explainer and entry page | `site/src/content/docs/proof/harness.md` |
| `/proof/journeys/` | journeys → tests explainer | `site/src/content/docs/proof/journeys.md` |
| `/proof/smoke/` | endpoint smoke explainer | `site/src/content/docs/proof/smoke.md` |

### 5.3 Standards, governance, and reference families

These route families are primarily owned by `site/src/content/docs/`.

| Family | Purpose |
| --- | --- |
| `/conformance/` | versioned conformance and standalone suite docs |
| `/getting-started/` | onboarding, quick start, concepts, implementor guidance |
| `/guides/` | implementation and migration guidance |
| `/governance/` | publication rules, release cadence, incident response, decision references |
| `/integrations/` | domain/adopter integration lanes |
| `/reference/` | resolver API reference |
| `/spec/v01/` and `/spec/v02/` | docs-hosted spec pages |
| `/publishing/` | deployment, changelog, domain split, production smoke, releasing |
| `/implementations/` | implementation index |
| `/handouts/` | staged narrative handout sequence |
| `/for-agents/` | public agent-facing onboarding/discovery routes |

### 5.4 Machine-readable discovery and static asset surfaces

| Public path family | Purpose | Source of truth |
| --- | --- | --- |
| `/.well-known/universal-manifest.json` | standards discovery descriptor | `site/public/.well-known/universal-manifest.json` |
| `/.well-known/security.txt` | security contact/disclosure | `site/public/.well-known/security.txt` |
| `/llms.txt` | agent-readable high-level summary | `site/public/llms.txt` |
| `/agent/fixture-catalog.json` | machine-readable fixture index | `site/public/agent/fixture-catalog.json` |
| `/agent/sandbox-scenarios.json` | machine-readable scenario index | `site/public/agent/sandbox-scenarios.json` |
| `/animations/...` | explainer SVG library | `site/public/animations/` |
| `/diagrams/...` | diagram library | `site/public/diagrams/` |
| `/tools/concept-explorer/...` | concept explorer UI/data | `site/public/tools/concept-explorer/` |
| `/sandbox/fixtures/...` | scenario fixture payloads | `site/public/sandbox/fixtures/` |
| `/sandbox/illustrations/...` | scenario illustrations | `site/public/sandbox/illustrations/` |
| `/ns/universal-manifest/...` | published schema/context namespace artifacts | generated site output from spec artifacts |

### 5.5 Internal-only review surfaces

These are intentionally not part of the public MVP front door.

| Route | Purpose |
| --- | --- |
| `/review/full-site-audit/` | route and surface inventory review page |
| `/review/reorganization-blueprint/` | staged public-surface reorganization blueprint |

## 6. `site/src/content/docs` Content-Family Map

The public docs corpus is primarily owned by the Starlight content tree.

| Content family | What it contains |
| --- | --- |
| `about/` | positioning, explainers, standards landscape, visuals |
| `conformance/` | conformance overview, resolver, standalone suite, version pages |
| `for-agents.md` and `external-agent-onboarding.md` | public agent onboarding/discovery material |
| `getting-started/` | adopt, concepts, quick start, implementation, stub manifests, helper, workbench |
| `governance/` | publication gates, release cadence, decisions, incident response, deprecation |
| `guides/` | implementation, migration, integration-authoring, quick reference |
| `handouts/` | compact staged reading sequence |
| `implementations/` | implementation index |
| `integrations/` | DID/VC, GPC, healthcare, metaverse, OMA Trust, RP1, smart glasses, smart home, social, reference runtime |
| `proof/` | harness, journeys, smoke |
| `publishing/` | changelog, deploy, domain split, production smoke, releasing, versioning |
| `reference/` | resolver API |
| `spec/` | docs-hosted `v0.1` and `v0.2` pages |
| `use-cases/` | app developer, creator, enterprise, privacy, venue operator |
| `index.md` | docs overview |

## 7. Interactive Tool Surfaces

These deserve separate treatment because they were built in different waves and now sit under the same higher-level shell family.

### 7.1 Sandbox

Purpose:

- scenario-driven browser proof
- validation, lane walkthroughs, adversarial cases

Current ownership:

- shell route: `site/src/pages/sandbox/index.astro`
- scenario routes: `site/src/pages/sandbox/[...scenario].astro`
- interactive components: `site/src/components/sandbox/`
- static assets: `site/public/sandbox/`

### 7.2 Workbench

Purpose:

- import, inspect, edit, validate, and export manifests directly in-browser

Current ownership:

- host shell: `site/src/pages/workbench/index.astro`
- compatibility redirect: `site/src/pages/workbench/index/index.astro`
- raw payload: `site/public/workbench/app/index.html`
- client logic: `site/public/workbench/workbench.js`

### 7.3 Harness

Purpose:

- quick manual endpoint and fixture checks

Current ownership:

- raw harness UI: `site/public/harness/index.html`
- reader-facing explainer route: `site/src/content/docs/proof/harness.md`

### 7.4 Learning hub

Purpose:

- tie tools and proof surfaces together coherently without widening the calm public front door

Current ownership:

- `site/src/pages/learning/index.astro`

## 8. Runtime Surface Map (`myum.net`)

The runtime service is owned by `services/myum-resolver/`.

Key runtime/public surfaces:

| Runtime path | Purpose |
| --- | --- |
| `GET /health` | service health |
| `GET /.well-known/myum-resolver.json` | runtime discovery descriptor |
| `GET /.well-known/security.txt` | resolver security contact |
| `GET /openapi.json` | resolver OpenAPI contract |
| `GET /{UMID_PATH}` | UMID resolution |

Runtime behavior includes:

- direct UMID resolution
- `b64u:` path decoding
- redirect and direct-payload record handling
- KV-backed storage
- fallback fixture behavior
- short cache semantics
- provenance and resolver headers

Primary runtime docs:

- `services/myum-resolver/README.md`
- `services/myum-resolver/CONTRACT.md`
- `services/myum-resolver/src/index.ts`

## 9. Evidence and Verification Surfaces

The project’s proof posture is unusually important. These surfaces make the project more than a static spec.

| Area | Purpose |
| --- | --- |
| `examples/` | baseline and adversarial fixtures |
| `conformance/` | implementation validation packaging |
| `packages/universal-manifest/scripts/` | smoke, terminology, sync, and verification scripts |
| `docs/journeys/` | canonical journeys mapped to executable proof |
| `/sandbox/` | browser-visible scenario proof |
| `/workbench/` | browser-visible authoring and validation |
| `/harness/index.html` | browser-visible quick endpoint/fixture checks |
| `packages/universal-manifest/scripts/smoke-endpoints.mjs` | endpoint smoke verification |

## 10. Governance and Memory Surfaces

These docs govern the whole program rather than a single subsystem.

| File or family | Role |
| --- | --- |
| `docs/README.md` | human/agent entry point to docs |
| `docs/STATE-OF-THE-PROJECT.md` | merged current-state snapshot |
| `docs/CRITICAL-PATH.md` | execution sequence and readiness framing |
| `docs/DECISIONS.md` | architectural decision history |
| `docs/workorders/` | scoped work-order ledger |
| `docs/workorders/WO-INDEX.md` | canonical WO index |
| `docs/reports/` | evidence and verification archive |
| `docs/PROJECT-VISION.md` | what UM is trying to enable |
| `docs/PUBLISHING-AND-VERSIONING.md` | publication policy |
| `docs/DOMAIN-ARCHITECTURE.md` | two-property split |
| `docs/DONE-DONE-*` | release-completion framework |

## 11. Current Posture

As of the current merged state:

- the project is no longer spec-only
- the homepage/spec split is complete
- the calm two-page public MVP is complete
- the first shared internal `UM UI` layer is complete
- the first reader reintegration wave is complete
- the first tool/proof reintegration wave is complete
- all formal work orders currently defined in `docs/workorders/` are complete

That means the project should now be understood less as a backlog in progress and more as a multi-surface system that must be kept coherent across:

- normative contract
- examples and conformance
- public docs and adoption surfaces
- interactive/browser-visible proof surfaces
- runtime resolver behavior
- governance and memory

## 12. Recommended Reading Order

If someone needs the deepest orientation in the least number of files, read in this order:

1. `README.md`
2. `docs/STATE-OF-THE-PROJECT.md`
3. `docs/COMPREHENSIVE-PROJECT-PROPERTIES-AND-SURFACES-MAP.md`
4. `docs/DOMAIN-ARCHITECTURE.md`
5. `docs/DECISIONS.md`
6. `spec/v0.1/README.md`
7. `spec/v0.1/CONFORMANCE.md`
8. `services/myum-resolver/CONTRACT.md`

## 13. Maintenance Rule

This document must be updated when any of the following changes:

- a new public property is introduced
- a major route family is added, removed, or re-homed
- a tool or proof surface changes ownership or entry path
- a runtime contract surface changes
- the project changes which repo area is the source of truth for a major surface family

This file is intended to stay stable and high-signal. It should describe structure, ownership, boundaries, and route families, not transient implementation chatter.
