# Universal Manifest — Spec Status Audit Evidence Appendix

Date: 2026-02-17  
Work Order: `docs/workorders/WO-0008-spec-status-scope-and-foundations-audit.md`

This appendix is a path-addressable evidence bundle for the claims in:

- `docs/reports/2026-02-12-spec-status-and-foundations-audit.md`

## 1) Repo inventory evidence

Normative surfaces (v0.1):

- `spec/v0.1/schema.jsonld`
- `spec/v0.1/schema.json`
- `spec/v0.1/README.md`
- `spec/v0.1/CONFORMANCE.md`
- `spec/v0.1/REGISTRY.md`

Fixtures (v0.1):

- Valid: `examples/v0.1/*.jsonld` and `examples/v0.1/stubs/*.jsonld`
- Invalid: `examples/v0.1/invalid/*.jsonld`

Tooling:

- TS helper + fixture validator: `packages/universal-manifest/`

## 2) Conformance harness evidence (runnable)

Command run:

- `cd packages/universal-manifest && npm test`

Observed result (summary):

- Valid fixtures: 9 accepted
- Invalid fixtures: 11 rejected (expected invalid)

For full output, rerun the command above (output is deterministic unless fixtures change).

## 3) Foundational references reviewed (UM repo)

Core scope and boundaries:

- `docs/DEPTH-AND-SCOPE.md`
- `docs/PROJECT-VISION.md`
- `docs/STATE-OF-THE-PROJECT.md`
- `docs/DECISIONS.md`
- `docs/CRUCIAL-DETAILS.md`

Done-done definition and gates:

- `docs/DONE-DONE-DEFINITION.md`
- `docs/DONE-DONE-CHECKLIST.md`
- `docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`

Publishing and domain split:

- `docs/DOMAIN-ARCHITECTURE.md`
- `docs/PUBLISHING-AND-VERSIONING.md`
- `docs/RELEASING.md`

Normative contract + conformance:

- `spec/v0.1/README.md`
- `spec/v0.1/schema.json`
- `spec/v0.1/schema.jsonld`
- `spec/v0.1/REGISTRY.md`
- `spec/v0.1/CONFORMANCE.md`

Integrity draft:

- `spec/v0.2/SIGNATURE-PROFILE.md`

## 4) reference implementation contextual evidence (copied in-repo for traceability)

These documents were produced earlier in the reference implementation repo and copied here verbatim as inputs:

- `docs/reports/inputs/reference-platform-universal-manifest/2026-02-13-spec-scope-and-done-definition.md`
- `docs/reports/inputs/reference-platform-universal-manifest/2026-02-13-spec-readiness-scorecard.md`
- `docs/reports/inputs/reference-platform-universal-manifest/2026-02-13-foundational-reference-crosswalk.md`
- `docs/reports/inputs/reference-platform-universal-manifest/2026-02-13-publishing-runbook-universalmanifest-net.md`
- `docs/reports/inputs/reference-platform-universal-manifest/2026-02-13-docs-site-ia-and-style.md`
- `docs/reports/inputs/reference-platform-universal-manifest/2026-02-13-reference-implementation-support-integration.md`

Original locations:

- `/Users/grig/work/repo/reference-platform/.dev/ai/reports/universal-manifest/`

## 5) External indexed references reviewed

GAS shared master index for Universal Manifest (maps where sources live on device):

- `/Users/grig/.agents/knowledge-sources/project-indexes/2026-02-13_10-03_universal-manifest_master-index.md`

External UM research archive (background inputs):

- `/Users/grig/Downloads/INBOX-markdown/universal-manifest/`

Review policy for this audit:

- Treated as background drivers and sanity checks, not normative requirements.
- The authoritative contract remains `spec/` within this repo.

