# WO-0160 -- Agent-Facing Content Completeness and Verification Gates

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-03-15

## Objective

Define the publication gates, verification rules, and completeness requirements for every agent-facing artifact so Universal Manifest does not ship fabricated, incomplete, stale, or weakly supported claims into its agent-facing surfaces.

## Context

If Universal Manifest is going to promote agent-friendly treatment as an adoption lever, it needs stronger quality gates than ordinary prose documentation. Agents will trust root-level files, well-known descriptors, and public guidance as contracts. That means incomplete or inflated claims become more damaging, not less.

This work order establishes the standards for when agent-facing content is allowed to exist and how it must be verified before publication.

## Scope

In scope:

1. Define what counts as an agent-facing artifact in this project, including:
   - landing-page agent paths
   - `llms.txt`
   - `skill.md`, if adopted
   - well-known descriptors
   - resolver contracts
   - machine-readable indexes
   - agent-oriented public documentation
2. Define completeness criteria for each artifact type.
3. Define anti-fabrication rules:
   - no unbacked capability claims
   - no dead-end routes
   - no partial contracts presented as finished surfaces
   - no ambiguous authority between standards host and runtime host
4. Define verification and freshness requirements:
   - ownership
   - source backing
   - verification steps
   - update cadence
   - machine-readable status or last-updated expectations where appropriate
5. Propose CI, review, or release gates that enforce these standards over time.

Out of scope:

- Full CI implementation for every proposed gate in this work order.
- A generic governance rewrite for the entire project.

## Deliverables

- Agent-facing publication gate framework.
- Verification checklist and review rubric for agent-facing artifacts.
- Proposed enforcement model for CI, release, or publishing workflow.
- Risk register for common failure modes: stale descriptors, overstated capability claims, incomplete onboarding, and unverifiable contracts.

Completed artifacts:

- `docs/reports/2026-03-15-agent-facing-publication-gates-framework.md`
- `site/src/content/docs/governance/agent-facing-publication-gates.md`
- `site/src/content/docs/for-agents.md`
- `site/astro.config.mjs`
- `site/scripts/sync-agent-discovery.mjs`
- `site/public/.well-known/universal-manifest.json`
- `site/public/llms.txt`

## Dependencies

- WO-0157 defines the target interaction surfaces.
- WO-0158 defines the discovery and machine-readable artifacts to be governed.
- WO-0159 defines the public documentation package that must pass these gates.

## Execution Notes

- The gate model should be explicit enough that future contributors cannot accidentally publish half-finished agent-facing surfaces.
- Verification should favor executable proof or direct artifact validation over prose assurances.
- This work order should end with a publish/no-publish decision framework for any future agent-facing addition.

## Acceptance Criteria

- [x] Agent-facing artifact classes are explicitly enumerated.
- [x] Each class has a defined completeness requirement and verification expectation.
- [x] The framework explicitly prevents fabricated, stale, or incomplete public claims.
- [x] A future contributor could use the resulting checklist to decide whether an agent-facing surface is ready to publish.
