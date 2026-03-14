---
status: COMPLETED
created: 2026-03-11T23:00:00Z
updated: 2026-03-11T23:30:00Z
owner: Standards Alignment
priority: P1
tags: [encryption, facets, privacy, jwe, selective-disclosure, deep-dive]
---

# WO-0153: Facet Visibility and Encryption Deep Dive — Report and Explainer

## Context
The Universal Manifest specification deliberately omits built-in encryption in v0.1/v0.2, keeping the base spec flexible and encouraging adopters to layer encryption above the protocol. Three visibility approaches have been established: projection model (normative), consent-based access control (normative), and encrypted inline facets (proposed, WO-0143, NOT_STARTED). External research into JWE, BBS+, SD-JWT, HPKE, and envelope encryption patterns has been conducted to identify where genuine gaps exist in the internal approach and to recommend standard-aligned solutions.

## Objective
Produce a comprehensive deep-dive report synthesizing internal project decisions (source of truth) with external standards research (gap-filling only), and create explainer materials suitable for video production targeting the OMA3 audience and security-minded evaluators.

## Deliverables
- [x] Comprehensive explainer document ([`docs/explainers/facet-encryption-deep-dive.md`](../explainers/facet-encryption-deep-dive.md))
- [x] NotebookLM video brief for L3-10 (embedded in explainer)
- [x] L3-10 added to production queue in Priority 1
- [x] Work order status updated to COMPLETED

## Dependencies
- WO-0143 (Private Encrypted Inline Facets vs Projection Model Analysis, NOT_STARTED) — this report informs but does not replace WO-0143
- Ed25519/JCS signing profile (v0.2, established)
- Consent model architecture (normative, established)
