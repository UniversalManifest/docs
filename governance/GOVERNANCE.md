# Universal Manifest Governance

**Version**: 1.0
**Effective Date**: 2026-02-27
**Status**: Active

## Purpose

This document defines the governance structure, decision-making processes, roles, and responsibilities for the Universal Manifest project. Universal Manifest is committed to open, transparent, and inclusive governance that serves the best interests of the specification and its adopters.

## Principles

1. **Open Development**: All development happens in public repositories with transparent discussion
2. **Meritocracy**: Contributions and expertise drive influence, not organizational affiliation
3. **Consensus-Seeking**: We strive for consensus while maintaining progress
4. **Interoperability First**: Technical decisions prioritize broad adoption and compatibility
5. **Evidence-Based**: Major decisions require implementation proof and real-world validation

## Project Scope

Universal Manifest is a standards-track specification for agent-to-agent and agent-to-human communication using structured manifest documents. The project includes:

- Normative specification documents
- JSON schemas and validation rules
- Conformance test suites
- Reference implementations and integration guides
- Documentation and adoption resources

## Roles and Responsibilities

### Contributors

Anyone who submits a contribution (code, documentation, issues, discussions) to the project.

**Responsibilities**:
- Follow the Code of Conduct
- Adhere to contribution guidelines
- Respect the RFC process for specification changes
- Provide constructive feedback

**How to become a contributor**: Submit a pull request or open an issue

### Maintainers

Individuals with commit access who review contributions, guide technical direction, and ensure project quality.

**Responsibilities**:
- Review and merge pull requests
- Triage and respond to issues
- Guide architectural decisions
- Ensure specification quality and consistency
- Uphold the done-done framework
- Mentor new contributors
- Participate in RFC review and approval

**How to become a maintainer**:
- Sustained high-quality contributions over 6+ months
- Deep understanding of the specification and its design goals
- Demonstrated technical judgment and collaboration skills
- Nomination by existing maintainer, approved by maintainer majority vote

**Current Maintainers**:
- Grig (grig@lumeneo.com) — Project Creator, Lead Maintainer

### Technical Steering Committee (TSC)

The TSC provides strategic direction, resolves disputes, and makes final decisions on contentious technical matters.

**Composition**: All active maintainers

**Responsibilities**:
- Approve or reject RFCs for specification changes
- Resolve technical disputes
- Define release criteria and maturity gates
- Approve new maintainers
- Update governance policies as needed

**Decision-Making**: Consensus-seeking with fallback to majority vote if consensus cannot be reached

### Project Lead

The Project Lead serves as primary coordinator and has tie-breaking authority in TSC deadlocks.

**Current Project Lead**: Grig (grig@lumeneo.com)

## Decision-Making Process

### Routine Decisions

Bug fixes, documentation improvements, and minor enhancements follow standard pull request review:

1. Submit pull request with clear description
2. At least one maintainer review required
3. Address feedback and resolve comments
4. Merge when approved

### Specification Changes

All changes to normative specification content require an RFC (Request for Comments):

1. Open an RFC issue using the RFC template
2. Community discussion period (minimum 7 days)
3. Address feedback and update proposal
4. TSC review and decision
5. If approved: implement in specification, tests, and documentation
6. Update relevant conformance tests

See [RFC-TEMPLATE.md](./RFC-TEMPLATE.md) for the RFC format.

### Breaking Changes

Changes that break backward compatibility require:

- RFC approval with explicit compatibility impact analysis
- Migration guide
- Deprecation period (where applicable)
- Major version bump

### Disputes

If consensus cannot be reached:

1. Attempt to find compromise through discussion
2. Escalate to TSC for review
3. TSC votes (simple majority required)
4. Project Lead has tie-breaking vote if needed

## Release Process

Universal Manifest follows semantic versioning (SEMVER):

- **Major (X.0.0)**: Breaking changes
- **Minor (0.X.0)**: New features, backward compatible
- **Patch (0.0.X)**: Bug fixes, clarifications

### Release Criteria

All releases must pass the done-done framework gates as defined in the [Done-Done documentation](../../site/src/content/docs/governance/done-done.md).

### Release Authority

- Patch releases: Any maintainer
- Minor releases: TSC consensus
- Major releases: TSC consensus + formal review period

## External Participation

### Registry Contributions

External entities can contribute registry entries (e.g., capability definitions, protocol extensions) following the [CONTRIBUTING-REGISTRY.md](./CONTRIBUTING-REGISTRY.md) process.

### Specification Feedback

We welcome feedback from:
- Implementers and adopters
- Adjacent standards bodies
- Security researchers
- End users

Submit feedback via:
- GitHub Issues (bug reports, feature requests)
- RFC proposals (specification changes)
- Mailing list discussions (planned)

## Code of Conduct

All participants must follow the [Code of Conduct](../../CODE_OF_CONDUCT.md). Violations should be reported to conduct@universalmanifest.net.

## Intellectual Property

Contributions are licensed under Apache License 2.0. By contributing, you agree to license your contributions under the same terms.

Patent claims: Contributors making specification proposals must disclose any known patent claims. The project follows Apache License 2.0 patent grant terms.

## Amendment Process

This governance document can be amended by:

1. Proposal via pull request
2. Discussion period (minimum 14 days)
3. TSC approval (2/3 majority required)
4. Version increment and effective date update

## References

- [Code of Conduct](../../CODE_OF_CONDUCT.md)
- [Contributing Guide](../../CONTRIBUTING.md)
- [RFC Template](./RFC-TEMPLATE.md)
- [Done-Done Framework](../../site/src/content/docs/governance/done-done.md)
- [Decision Log](../../site/src/content/docs/governance/decisions.md)

---

**Questions or feedback?** Open an issue or contact maintainers at maintainers@universalmanifest.net
