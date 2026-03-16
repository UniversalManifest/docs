# External Agent Onboarding and Adoption Memo

**Date:** 2026-03-15
**Related work order:** `WO-0159`
**Status:** Defined the external-agent onboarding package and adoption argument

## Summary

Universal Manifest now has a clearer story for how to introduce the project to agents in the wild and why doing so should help adoption rather than merely add another documentation layer.

The central claim is that agent-friendly treatment increases adoption only if it reduces ambiguity, reduces reverse engineering, and increases the rate at which outside evaluators and implementers reach correct conclusions from public materials.

## What Shipped

### Public onboarding path

- Added `site/src/content/docs/for-agents/external-agent-onboarding.md`
- Expanded `site/src/content/docs/for-agents/index.md` so the onboarding path and gate model are part of the visible agent entry route
- Updated the docs sidebar to expose a real multi-page `For Agents` section
- Added onboarding and gate links to discovery-facing materials

### Internal adoption story

This memo is the internal articulation of the argument for agent-friendly public treatment. It should be used when explaining the strategy to colleagues, partners, and implementers.

## Why This Should Increase Adoption

Agent-friendly treatment is useful only if it changes the cost structure of evaluation and implementation.

The adoption case is:

1. **Lower time to first correct understanding.**
   External agents can start from a descriptor, `llms.txt`, and an explicit onboarding path instead of scraping prose and UI.

2. **Lower research and integration friction.**
   Agents can move directly from discovery to schemas, conformance materials, resolver contract docs, and public examples.

3. **Higher-quality machine-mediated summaries.**
   When authoritative routes are explicit, outside agents are more likely to cite real docs and less likely to invent unsupported features.

4. **More repeatable external evaluation.**
   Different agents inside different organizations can follow the same entry path and arrive at comparable conclusions.

5. **Better conversion from curiosity to implementation.**
   The public path now routes from landing to docs to fixtures to proof to runtime, which shortens the path from "what is this?" to "I can test this."

## How To Introduce UM To Agents In The Wild

The project should use a minimal, repeatable seed packet:

- project description
- host split
- stable versus draft version posture
- canonical discovery URLs
- unsupported interaction modes
- task-specific next URLs based on whether the goal is understanding, implementation, runtime verification, or proof exploration

This is intentionally smaller than a full briefing. The goal is to make the first agent pass correct, not exhaustive.

## Distribution Channels

The package should be introduced through surfaces already under project control:

- landing page and `/docs/`
- `/for-agents/` and `/for-agents/external-agent-onboarding/`
- `/.well-known/universal-manifest.json`
- `/llms.txt`
- repo-facing partner and outreach materials

The project should avoid promising vendor-specific integrations until there is an actual maintained path for them.

## Signals To Measure

If this strategy is working, we should see measurable changes such as:

- traffic to `/.well-known/universal-manifest.json`, `/llms.txt`, and `/for-agents/`
- traffic from those pages into implementation docs, conformance docs, and resolver docs
- use of fixture and scenario catalogs instead of manual bundle scraping
- higher-quality external summaries that correctly describe the standards host versus runtime host split
- more external issues, questions, or prototypes that start from the correct public contracts
- reduced correction rate when outside agents describe current capabilities

## What Would Falsify The Claim

The strategy is not working if:

- agents still hallucinate the basic host split and capability posture
- traffic rises but correct implementation or evaluation behavior does not
- the project adds agent-facing surfaces faster than it can keep them current
- onboarding docs become another layer of prose that agents ignore

## Operating Constraint

This strategy only works if the public agent path stays honest and well verified. The moment the project publishes incomplete or inflated agent-facing surfaces, the same discoverability improvements will accelerate bad understanding instead of good adoption.

## Verification

- `cd /Users/grig/work/repo/universalmanifest/site && npm run build` -> PASS
- Browser verification confirmed:
  - `/for-agents/external-agent-onboarding/` renders and is linked from the `For Agents` sidebar group
  - `/governance/agent-facing-publication-gates/` is reachable as the next governance step from the onboarding path
  - the new public pages loaded without console errors

## Residual Warning

- The site build currently emits a duplicate-content-id warning for `for-agents/index.md`. The routes themselves work, but the warning remains and should be cleaned up in a follow-up pass if we want the Starlight content build fully warning-free.
