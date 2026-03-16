# Agent-Facing Publication Gates Framework

**Date:** 2026-03-15
**Related work order:** `WO-0160`
**Status:** Defined the publication gate model for agent-facing surfaces

## Summary

Universal Manifest now has an explicit gate framework for agent-facing artifacts.

The key decision is simple: if a surface is easy for an agent to trust, it must be treated like a contract. That means no fabricated capability claims, no dead-end routes, no authority ambiguity between `universalmanifest.net` and `myum.net`, and no publication without executable or directly inspectable evidence.

## Agent-Facing Artifact Classes

This framework governs the following classes:

- landing and agent-entry routes
- `llms.txt`
- `/.well-known` descriptors
- runtime descriptors and OpenAPI
- machine-readable fixture and scenario catalogs
- agent-oriented public documentation
- public tool surfaces when used as part of the agent path

## Gate Model

Every agent-facing artifact must pass five gate families before publication:

### G-A1: Authority clarity

The artifact must say which host owns the behavior, which source is canonical, and whether the surface is standards, tooling, or runtime.

### G-A2: Completeness

The artifact must be usable end to end. It cannot point at missing routes, undocumented prerequisites, or private internal knowledge.

### G-A3: Verification

Claims must be backed by a build, a test, a smoke check, a browser validation pass, or a generated artifact traceable to source. Prose assurance alone is insufficient.

### G-A4: Freshness

Version posture, last-updated values, route indexes, and catalog contents must be current. Any change to discovery order, route ownership, or public examples requires corresponding discovery updates.

### G-A5: Status honesty

Stable, draft, deferred, unsupported, experimental, read-only, and non-normative states must be explicit whenever omission would cause an agent to overstate current capability.

## Artifact-Specific Minimums

### Discovery files

`llms.txt` and well-known descriptors must:

- resolve all referenced URLs
- reflect the actual landing/docs/discovery split
- state the standards host versus runtime host split
- explicitly list unsupported interaction modes when relevant

### Machine-readable catalogs

Fixture and scenario catalogs must:

- be generated from source, not manually assembled
- include generation date and counts
- point only to public files and routes that actually exist
- remain consistent with the browser-visible tools they describe

### Runtime contracts

Resolver descriptors and OpenAPI must:

- match live runtime behavior
- stay aligned with the resolver docs
- be covered by tests or smoke validation
- avoid implying write or task lifecycle behavior that does not exist

### Agent-oriented docs

Agent guidance pages must:

- identify authoritative sources in order
- distinguish normative, supportive, and future-facing material
- route readers to the correct host and contract layer
- avoid productizing undeployed or experimental paths

### Tool-surface claims

Any claim about Sandbox, Harness, Workbench, or Resolver UI must be limited to what the tool actually demonstrates. Browser tools do not become normative merely because they are public.

## No-Publish Conditions

Do not publish or promote an agent-facing artifact if any of the following are true:

- it claims a public capability that is not live
- it references a route or file that does not resolve
- it collapses the standards host and runtime host into one implied authority
- it presents draft or deferred capabilities as stable
- it has no current evidence path
- it requires scraping bundles or guessing hidden behavior to complete the documented workflow

## Required Verification Workflow

Minimum verification for future agent-facing changes:

1. Regenerate discovery and catalog artifacts when their source inputs change.
2. Run `cd /Users/grig/work/repo/universalmanifest/site && npm run build`.
3. If resolver surfaces changed, run:
   - `cd /Users/grig/work/repo/universalmanifest/services/myum-resolver && npm test`
   - `cd /Users/grig/work/repo/universalmanifest/services/myum-resolver && npm run typecheck`
4. Browser-verify each changed public page and each changed machine-readable route.
5. Cross-check freshness-sensitive claims against the changelog and current version posture.

## Proposed Enforcement

This work order does not implement full CI enforcement, but it does define the desired model:

- keep discovery catalogs generated from source files, not hand-maintained
- fail review when public agent-facing routes are added without explicit authority and status language
- fail review when `llms.txt`, descriptors, and public docs disagree on supported interaction modes
- fail review when agent-oriented docs reference routes absent from the built site
- require evidence references in work-order closeout whenever agent-facing artifacts change

## Risk Register

Primary failure modes to watch:

- stale descriptors after route changes
- `llms.txt` drift from the actual public route order
- runtime docs overstating resolver capabilities
- onboarding docs that omit stable versus draft posture
- tool pages being mistaken for normative contracts
- future agent-service ideas being described as current surfaces

## Result

Future contributors now have a publish/no-publish framework for any agent-facing addition. The practical rule is that agent-facing material must be narrower, clearer, and better verified than ordinary explanatory prose.

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- Browser verification confirmed:
  - `/governance/agent-facing-publication-gates/` renders and is linked from the `For Agents` sidebar group
  - the page loads without console errors

## Residual Warning

- The current Starlight build emits a duplicate-content-id warning for `for-agents/index.md`, but the built `/for-agents/` and `/for-agents/external-agent-onboarding/` routes render correctly. This needs follow-up if we want a warning-clean build, but it did not block the published routes in this pass.
