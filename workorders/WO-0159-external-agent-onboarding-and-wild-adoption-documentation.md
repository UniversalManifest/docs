# WO-0159 -- External Agent Onboarding and Wild Adoption Documentation

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-03-15

## Objective

Create the documentation package that introduces Universal Manifest to external agents "in the wild," explains how they should interact with the standard and its public surfaces, and gives the project a clear, defensible adoption story for colleagues, partners, and implementers.

## Context

Improving agent discoverability alone is not enough. Universal Manifest also needs explicit documentation explaining:

- what agents should do first
- which surfaces are authoritative
- how to move from overview to schema to resolver to fixtures to tools
- how to avoid misusing partial or non-normative surfaces
- why this public treatment should plausibly increase adoption

This work order covers both project-internal documentation and outward-facing playbooks that make the agent path legible and reproducible.

## Scope

In scope:

1. Define the public "For Agents" content path for Universal Manifest.
2. Create or expand project documentation covering:
   - authoritative sources for agents
   - recommended read-only workflows
   - resolver usage
   - schema and fixture discovery
   - tool usage boundaries for sandbox, harness, and workbench
3. Document how Universal Manifest should be introduced to external agents and agent ecosystems.
4. Document the argument for why agent-friendly treatment should improve adoption, including what signals to measure.
5. Clarify where standards guidance ends and runtime/implementation behavior begins.

Out of scope:

- Full execution of every outreach/integration into third-party agent ecosystems.
- Vendor-specific prompt packs for every model provider.
- Rewriting the full documentation site in one pass.

## Deliverables

- Project documentation package for external-agent onboarding.
- Public-facing agent path narrative for the website.
- Adoption-story memo or equivalent internal-facing document for stakeholder alignment.
- Guidance on how to present UM to external agents without overstating current capabilities.

Completed artifacts:

- `docs/reports/2026-03-15-external-agent-onboarding-and-adoption-memo.md`
- `site/src/content/docs/for-agents/external-agent-onboarding.md`
- `site/src/content/docs/for-agents/index.md`
- `site/src/content/docs/governance/agent-facing-publication-gates.md`
- `site/astro.config.mjs`
- `site/scripts/sync-agent-discovery.mjs`
- `site/public/.well-known/universal-manifest.json`
- `site/public/llms.txt`

## Dependencies

- WO-0157 defines the surface model.
- WO-0158 defines the discovery artifacts and machine-readable entry points the documentation must point to.

## Execution Notes

- This documentation should let an external agent onboard with minimal ambiguity.
- Public docs must remain explicit about which surfaces are normative, non-normative, experimental, or future-facing.
- The documentation should be written so a colleague can use it to defend the adoption argument without hand-waving.

## Acceptance Criteria

- [x] A dedicated documentation path exists for external agents.
- [x] The path explains what is authoritative, what is optional, and what is future-facing.
- [x] The docs tell agents how to use the standards host, the resolver, and the tool surfaces without mixing their roles.
- [x] The repo contains a clear project-internal articulation of the adoption argument and its measurable signals.
