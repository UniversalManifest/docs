# Multi-Surface Agent-Friendly Architecture for Universal Manifest

**Date:** 2026-03-15
**Related work order:** `WO-0157`
**Status:** Approved target-state architecture and execution sequence

## Executive Summary

Universal Manifest should evolve from a docs-first public surface into a multi-layer public system with different entry paths for:

- humans evaluating the standard
- implementers integrating the standard
- agents discovering, verifying, and using the standard
- browser users exploring the tooling and proof surfaces

This does **not** require turning `universalmanifest.net` into an agent runtime.

Instead, the correct model is:

1. `universalmanifest.net` becomes the **landing + standards + tooling + agent-discovery host**.
2. `myum.net` remains the **runtime resolver contract host**.
3. Any future higher-agency agent service gets its **own host or subdomain**, rather than collapsing the standards site and runtime/service concerns into one surface.

This preserves the existing standards/runtime split while expanding Universal Manifest into a stronger public adoption surface.

## Why this change is needed

The current public experience is effective for readers who already intend to consume documentation, but it is weaker for:

- first-time evaluators who need a clear landing experience
- agents that need predictable discovery entry points
- colleagues and partners who need to understand the full public-surface strategy
- future adoption work that needs a clear separation between overview, reference, tooling, and runtime

The project already has strong raw material:

- a live standards site
- a live resolver contract
- schema and JSON-LD artifacts
- a sandbox, harness, and workbench
- agent-oriented briefing material

What is missing is a governing architecture that turns those pieces into a coherent outside-in system.

## Existing constraints that must remain true

### 1. Standards host and runtime host stay separate

The current domain split remains correct:

- `universalmanifest.net` is the canonical standards/docs host
- `myum.net` is the canonical resolver/runtime host

The new architecture must strengthen that split, not weaken it.

### 2. Universal Manifest remains spec-first

Public UX can expand far beyond documentation, but the project still needs to present the specification as the source of truth. Tooling, demos, and agent-facing surfaces must never quietly replace the spec.

### 3. Agent support starts as low-agency, read-mostly support

The first public agent path should help agents:

- find the right pages
- fetch machine-readable artifacts
- understand the resolver contract
- use the public tooling and proof surfaces

The first phase should **not** add task claiming, agent identity exchange, message signing, or other runtime-style behavior.

## Target surface model

### Layer A -- Root discovery and machine-readable contract layer

This is the public discovery layer for both humans and agents.

Primary surfaces:

- `/.well-known/universal-manifest.json`
- `/.well-known/security.txt`
- `llms.txt`
- optional `skill.md` if the project chooses a formal agent onboarding file
- machine-readable fixture/scenario/tool indexes where justified

Purpose:

- let agents and integrators discover the project without scraping prose or browser bundles
- make canonical routes explicit
- define what is real, authoritative, and supported

### Layer B -- Landing and audience-routing layer

This becomes the new role of `/`.

Purpose:

- present Universal Manifest as a standard worth adopting
- route different audiences into the correct next step quickly
- stop forcing all users to begin with the docs shell

Required audience lanes:

- evaluators / decision-makers
- implementers
- agents
- proof/tool explorers

This landing surface should be short, opinionated, and navigational. It should not duplicate the full reference material.

### Layer C -- Documentation and reference layer

This becomes the secondary page set rather than the primary home experience.

Target posture:

- full docs/reference center
- specification, conformance, governance, guides, integrations
- agent-facing reference pages and public onboarding docs

Recommended route model:

- move the docs home to `/docs/`
- keep route compatibility for existing published paths during migration
- maintain stable deep links for current content

The migration may use redirects, mirrored entry points, or staged route changes, but the target-state concept is clear: **landing first, docs second**.

### Layer D -- Tooling and proof layer

This layer remains on `universalmanifest.net`, but should be treated as a first-class public interaction tier rather than a side attachment to the docs.

Included surfaces:

- sandbox
- harness
- workbench
- resolver UI proxy/explainer surfaces on the docs domain, if retained

Purpose:

- provide practical exploration and proof
- show how the standard behaves in use
- support both human exploration and bounded agent/browser automation

These surfaces should gain explicit machine-readable indexes and deep-link contracts where appropriate.

### Layer E -- Immutable standards artifact layer

This remains the stable artifact host under `/ns/universal-manifest/...`.

Purpose:

- canonical JSON-LD contexts
- canonical JSON Schemas
- stable versioned artifact URLs

This layer should remain extremely conservative and stable.

### Layer F -- Runtime resolver layer

This remains on `myum.net`.

Purpose:

- UMID resolution
- resolver runtime contract
- health and well-known runtime descriptor
- machine-readable resolver contract and public API reference

This layer should continue to be read-mostly and deterministic.

### Layer G -- Future higher-agency service layer

If Universal Manifest later needs:

- authenticated agent services
- task-oriented APIs
- A2A messaging
- agent identity and signing
- higher-agency writes or workflow orchestration

those capabilities should live on a future dedicated service host or subdomain, not on the standards host by default.

This keeps the standards site clean and protects the domain split.

## Domain-to-layer assignment

### `universalmanifest.net`

Owns:

- Layer A: root discovery
- Layer B: landing
- Layer C: docs/reference
- Layer D: tools/proof
- Layer E: immutable standards artifacts

Does not own:

- resolver lookup as a primary runtime contract
- authenticated agent runtime behavior
- high-agency A2A or MCP service semantics

### `myum.net`

Owns:

- Layer F: runtime resolver contract
- runtime well-known descriptor
- runtime API contract exposure
- runtime operational posture

Does not own:

- long-form standards marketing
- full governance and reference navigation
- multi-audience landing content beyond minimal runtime orientation

### Future host or subdomain

Owns:

- Layer G only, if and when Universal Manifest chooses to expose higher-agency services

Candidate examples:

- `agents.universalmanifest.net`
- `api.universalmanifest.net`
- a separate product/service domain

## Interaction modes by audience

### Human evaluator

Path:

1. landing page
2. one-pager / full briefing / use cases
3. adoption proof and governance
4. selective tool exploration if needed

Goal:

- understand why Universal Manifest matters
- understand why it is credible
- understand why the public architecture is professional and durable

### Implementer

Path:

1. landing page or direct discovery contract
2. docs/reference
3. schema + conformance + guides
4. resolver contract
5. tooling and proof

Goal:

- adopt the standard or build against it quickly

### Agent

Path:

1. root discovery files
2. agent-facing reference path
3. schemas, fixtures, and resolver contract
4. tooling/proof surfaces with explicit deep links and indexes

Goal:

- discover authoritative surfaces quickly
- avoid guessing
- perform bounded, read-mostly interaction correctly

### Tool/proof explorer

Path:

1. landing page or docs/tools route
2. sandbox/harness/workbench
3. related reference docs and proof docs

Goal:

- see the standard in action
- validate how it behaves

## What should not happen

The public architecture should explicitly avoid:

- turning `universalmanifest.net` into a general-purpose agent runtime
- mixing standards authority with high-agency service behavior
- adding discovery files that point to incomplete or speculative routes
- publishing agent-facing guidance without proof or verification backing
- using the resolver host as a substitute for the standards site

## Adoption hypothesis

The point being proved is:

> A project that treats agents as first-class discoverers and readers of its public surfaces should lower integration friction and improve adoption.

That claim is defensible if Universal Manifest improves the following:

- time to first successful discovery of canonical artifacts
- time to first valid resolver interaction
- time to first valid schema-backed integration step
- number of public surfaces that can be used without manual interpretation
- reduction in agent prompt/context overhead required to onboard
- reduction in ambiguity about which surface is authoritative

These measures should be refined under WO-0159 and WO-0160.

## Execution sequence

### Phase 1 -- Architecture authority

Execute first:

- `WO-0157`

Purpose:

- define the target system before implementation fragments it

### Phase 2 -- Discovery and public entry points

Execute second:

- `WO-0158`

Purpose:

- make the public surfaces discoverable and machine-usable

### Phase 3 -- Landing/docs split implementation

Execute third:

- `WO-0161`

Purpose:

- implement the new landing-first experience and move the docs experience into a clearly secondary path

### Phase 4 -- Agent onboarding and adoption narrative

Execute fourth:

- `WO-0159`

Purpose:

- make the new architecture understandable and usable by external agents and internal stakeholders

### Phase 5 -- Publication gates and enforcement

Execute fifth:

- `WO-0160`

Purpose:

- ensure agent-facing artifacts are complete, current, and verified before broad publication

## Additional work order required

The current program needs one more implementation work order:

- `WO-0161 -- Landing Page and Docs Secondary Route Implementation`

Reason:

- the current WO set covers architecture, discovery, documentation, and gates
- it does **not** yet include the explicit implementation work needed to make `/` a landing page and move docs into a secondary experience

That work should now be tracked explicitly rather than implied.

## Decision

Universal Manifest should move forward as a **multi-surface public system** with:

- landing
- docs/reference
- tools/proof
- machine-readable discovery
- stable artifact hosting
- resolver runtime hosting

but **without** turning the standards host into an agent runtime.

That is the architecture that best supports adoption, preserves the standards boundary, and creates a credible agent-first public posture.
