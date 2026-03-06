# WO-0136 — OMB Wiki Spatial Fabric Source Refresh and Primary-Source Crosscheck

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Research Intake and Integration Architecture  
**Source:** `https://omb.wiki`, `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`, `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md`

## Objective

Verify whether the Open Metaverse Browser Wiki (`omb.wiki`) contains any meaningful spatial-fabric detail that is not already reflected in the current RP1/UM integration work, while preserving the rule that primary repositories and specifications remain authoritative when the wiki is incomplete or behind reality.

## Problem Statement

Universal Manifest already has an RP1 spatial-fabric lane, fixture coverage, and journey evidence from the earlier RP1 ingestion wave. However, the Open Metaverse Browser Wiki is a newer ecosystem map that may expose additional spatial-fabric concepts, terminology, or source links that should inform later Research-First decisions. The wiki itself explicitly presents as a “capture first, organize second, curate continuously” resource grounded in primary sources, so this work must distinguish discovery value from source-of-record value.

## Scope

In scope:

- Audit `https://omb.wiki` for spatial-fabric, open-spatial-internet, and RP1-adjacent material relevant to Universal Manifest.
- Compare wiki-discovered material against:
  - `/Users/grig/work/repo/universalmanifest/integrations/rp1-spatial-fabric.md`
  - `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md`
  - existing RP1 fixtures, journeys, and localized source records.
- Identify:
  - already-covered concepts,
  - newly surfaced concepts or source pointers,
  - and any places where a primary-source refresh is warranted.
- Produce a recommendation on whether follow-on RP1/spatial-fabric documentation or research work is needed.

Out of scope:

- Directly rewriting the RP1 integration lane before the audit is complete.
- Treating the wiki as a normative or primary authority when repositories/specs provide stronger evidence.
- New normative spec changes.

## Deliverables

- A new report under `/Users/grig/work/repo/universalmanifest/docs/reports/`
- Governance/status synchronization only if the audit creates new follow-on work

## Acceptance Criteria

- [x] The report explicitly states what `omb.wiki` adds beyond current UM RP1 material, if anything.
- [x] Wiki-discovered concepts are separated from primary-source-confirmed concepts.
- [x] The report gives a clear recommendation: no action, doc refresh, source refresh, or new follow-on work order.
- [x] The sequencing note is preserved: this audit should inform later spatial-fabric or federation decision work rather than arrive after it.

## Dependencies

- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0020-rp1-source-ingestion-and-synthesis-materialization.md`
- `/Users/grig/work/repo/universalmanifest/docs/workorders/WO-0133-protocol-recommendation-governance-and-standards-currency-matrix.md`

## Sequencing Note

- Queue this work after `WO-0134` and before `WO-0135` so it can inform the broader federation/bridge decision package without blocking the unrelated proximity assessment.

## Execution Notes

- Completed on 2026-03-06.
- Delivered report: `/Users/grig/work/repo/universalmanifest/docs/reports/2026-03-06-omb-wiki-spatial-fabric-crosscheck.md`
- Outcome:
  - The current UM core boundary for RP1/MSF remains correct.
  - `omb.wiki` is valuable as a discovery map, not as the source of record.
  - The strongest resulting recommendation is a primary-source refresh and then an RP1/MSF documentation/proof refresh.
