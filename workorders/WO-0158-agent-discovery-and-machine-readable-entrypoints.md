# WO-0158 -- Agent Discovery and Machine-Readable Entry Points

**Status:** COMPLETED
**Priority:** P0
**Created:** 2026-03-15

## Objective

Make Universal Manifest discoverable and operable by external agents through predictable root-level files, well-known descriptors, route taxonomy, and machine-readable public entry points across `universalmanifest.net` and `myum.net`.

## Context

If Universal Manifest is going to prove that agent-friendly treatment can improve adoption, the public surfaces cannot rely on agents scraping prose and reverse-engineering browser code. The standards host and resolver host need explicit discovery and interaction contracts.

This work order covers the machine-readable layer that sits beneath the landing page and documentation UX.

## Scope

In scope:

1. Define and publish the minimum discovery layer for `universalmanifest.net`, including:
   - `llms.txt`
   - `/.well-known/security.txt`
   - enriched `/.well-known/universal-manifest.json`
   - a visible public "For Agents" path or equivalent route taxonomy
2. Define and publish the minimum discovery layer for `myum.net`, including:
   - runtime-appropriate `/.well-known/security.txt`
   - enriched resolver descriptor
   - canonical machine-readable resolver contract exposure
   - OpenAPI or equivalent public API contract for the resolver if justified
3. Define whether `skill.md` is required for Universal Manifest's public surfaces and, if so, what its scope should be.
4. Publish machine-readable indexes for public fixtures, scenarios, or tool surfaces where agents otherwise have to scrape JS bundles.
5. Ensure the resulting discovery layer reinforces the standards/runtime split instead of blurring it.

Out of scope:

- Contributor task feeds such as `tasks.json`, unless explicitly chosen as a separate program.
- A2A task lifecycle endpoints.
- WebMCP or browser-native MCP integration.

## Deliverables

- Discovery artifact inventory for both domains.
- Machine-readable public entry points for standards and resolver layers.
- Public route taxonomy for human and agent access paths.
- Gap report listing anything still blocking first-class agent discovery.

Completed artifacts:

- `docs/reports/2026-03-15-agent-discovery-and-machine-readable-entrypoints-report.md`
- `site/public/llms.txt`
- `site/public/.well-known/security.txt`
- `site/public/.well-known/universal-manifest.json`
- `site/public/agent/fixture-catalog.json`
- `site/public/agent/sandbox-scenarios.json`
- `site/src/content/docs/for-agents.md`
- `services/myum-resolver/src/index.ts`

## Dependencies

- WO-0157 must define the target architecture and domain boundaries first.

## Execution Notes

- Discovery artifacts must be treated as canonical public contracts, not marketing accessories.
- The implementation should prefer read-only, clearly scoped, low-agency interactions first.
- No discovery file may claim an interaction path that lacks a real backing surface, verification path, or ownership model.

## Acceptance Criteria

- [x] `universalmanifest.net` has a defined, explicit discovery layer for agents.
- [x] `myum.net` has a defined, explicit discovery layer for runtime/resolver interaction.
- [x] Public agent entry points no longer depend on scraping browser JS or guessing canonical docs.
- [x] The standards host and runtime host expose different but complementary discovery contracts.
