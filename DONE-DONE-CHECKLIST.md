# Universal Manifest — Done-Done Checklist

Use this checklist to evaluate whether a target release is actually done.

Primary definition: `docs/DONE-DONE-DEFINITION.md`

## 1) Release metadata

- [ ] Target version identified (example: `v0.1.1`, `v0.2.0`, `v1.0.0`)
- [ ] Target maturity identified (`Early-adopter`, `Production-candidate`, `World-ready`)
- [ ] Release owner identified
- [ ] Review date recorded

## 2) Gate G1 — Contract completeness

- [ ] Required fields and semantics are explicit in versioned spec docs
- [ ] Unknown-field handling and extension behavior are explicit
- [ ] Compatibility rules are explicit
- [ ] Registry entries updated for new standardized names
- [ ] Contract changes recorded in `docs/DECISIONS.md`

Evidence paths:

- [ ] `spec/v*/README.md`
- [ ] `spec/v*/schema.json`
- [ ] `spec/v*/schema.jsonld`
- [ ] `spec/v*/REGISTRY.md`
- [ ] `docs/DECISIONS.md`

## 3) Gate G2 — Conformance testability

- [ ] Consumer obligations are explicit
- [ ] Issuer obligations are explicit
- [ ] Valid fixtures cover required baseline scenarios
- [ ] Invalid fixtures cover required failure cases
- [ ] Validation harness passes valid fixtures
- [ ] Validation harness fails invalid fixtures

Evidence paths:

- [ ] `spec/v*/CONFORMANCE.md`
- [ ] `examples/v*/`
- [ ] test output attached in evidence pack

## 4) Gate G3 — Integrity and trust profile

- [ ] Integrity profile status is explicit for the target version
- [ ] Canonicalization behavior is explicit if signature behavior is normative
- [ ] Verification failure behavior is explicit
- [ ] Signature/verification fixtures exist when required

Evidence paths:

- [ ] `spec/v*/` integrity profile document(s)
- [ ] fixture and validation outputs in evidence pack

## 5) Gate G4 — Interoperability proof

- [ ] At least one end-to-end integration path is verified
- [ ] Cross-system projection/pointer behavior is documented
- [ ] Guidance is understandable for non-LAN adopters
- [ ] No LAN-only assumptions appear in normative contract text

Evidence paths:

- [ ] `integrations/lan.md`
- [ ] `integrations/social.md`
- [ ] integration test or walkthrough evidence in pack

## 6) Gate G5 — Publishing and discoverability

- [ ] Canonical URLs and versioning policy are documented
- [ ] Release process is documented
- [ ] Docs index includes a clear first-time reader path
- [ ] Artifact stability/immutability policy is documented

Evidence paths:

- [ ] `docs/PUBLISHING-AND-VERSIONING.md`
- [ ] `docs/RELEASING.md`
- [ ] `docs/README.md`

## 7) Gate G6 — Governance and change control

- [ ] Major decisions recorded with rationale
- [ ] Breaking-change handling is explicit
- [ ] Deprecation and migration policy is explicit
- [ ] No unresolved policy contradictions across docs

Evidence paths:

- [ ] `docs/DECISIONS.md`
- [ ] release notes / migration docs in evidence pack

## 8) Gate G7 — Operational realism

- [ ] Local-first and partial connectivity assumptions are addressed
- [ ] TTL/cache/log-reference behavior is clear
- [ ] Explicit out-of-scope list prevents overbuild
- [ ] Operational guidance and normative contract are aligned

Evidence paths:

- [ ] `docs/STATE-OF-THE-PROJECT.md`
- [ ] `docs/DEPTH-AND-SCOPE.md`
- [ ] `integrations/lan.md`

## 9) Additional checks for World-ready claims

- [ ] Three or more independent organizations have successful implementations
- [ ] At least two external implementations are outside originating ecosystem
- [ ] Conformance suite includes adversarial and misuse cases
- [ ] Long-term governance and release cadence are demonstrated
- [ ] Incident/rollback procedures are documented and tested

## 10) Final sign-off

- [ ] Evidence pack completed (`docs/DONE-DONE-EVIDENCE-PACK-TEMPLATE.md`)
- [ ] All required gates for target maturity are pass
- [ ] Deferrals are explicitly listed with owner and date
- [ ] Approvers sign off with date and role

No final sign-off means done-done is not achieved.
