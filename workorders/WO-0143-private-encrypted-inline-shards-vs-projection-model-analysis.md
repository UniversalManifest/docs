# WO-0143 — Private Encrypted Inline Facets vs. Projection Model Analysis

**Status:** NOT_STARTED  
**Created:** 2026-03-07  
**Updated:** 2026-03-07  
**Priority:** P1  
**Owner:** Universal Manifest Architecture  

## Objective

Deeply reconsider the treatment of private data in the Universal Manifest, specifically evaluating the current Projection model against allowing encrypted inline JSON facets as an option (or supporting both) in a universal, non-opinionated manner.

## Problem Statement

Currently, the Universal Manifest handles privacy primarily through Selective Disclosure / Projection (creating a derived manifest with only the allowed subsets of data for a specific Consumer). However, relying entirely on projection introduces complex lifecycle problems: Where does a new projection come from if requirements change? At the same time, offering encrypted inline facets within the manifest poses challenges with key rotation, obsolescence, and payload size. Both models have validity, and UM needs multiple, flexible ways of handling private data to remain truly universal.

## Scope

In scope:
- Deep architectural analysis comparing the Projection model with Inline Encrypted Facets.
- Investigating the lifecycle of projections (how consumers request new projections dynamically).
- Investigating key management for encrypted facets (key rotation, removing obsolete data, revocation).
- Formulating a flexible standard that allows multiple valid ways of handling this without forcing an overly opinionated design on adopters.

Out of scope:
- Dropping projection entirely.
- Forcing a single mandatory encryption algorithm on all issuers.
- Renaming existing facets (formerly shards) in the core spec — that is tracked separately.

## Deliverables

- Architectural decision report (ADR) detailing the paths for handling private/sensitive data seamlessly.
- Proposed updates to the core UM specification or guidance around encrypted facets.
- Code fixtures demonstrating the lifecycle of an encrypted facet (and its key).

## Dependencies

- None.

## Execution Notes

- This is a critical architectural decision. The solution must be universal and provide multiple ways of handling private data securely, addressing the operational reality of managing keys and dynamic data requests over time.
- Note: "facets" is the current term for what was previously called "shards" in the UM spec.
