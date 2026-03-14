# WO-0129 — Universal Manifest Inbox Dedupe, Import, and Archive

**Status:** COMPLETED  
**Created:** 2026-03-06  
**Updated:** 2026-03-06  
**Priority:** P1  
**Owner:** Documentation + Knowledge Corpus Hygiene  
**Source:** `/Users/grig/Downloads/INBOX-markdown/`

## Objective

Run a two-pass ingestion sweep over the Universal Manifest-related inbox corpus so the project has one authoritative answer for each source: already localized, newly localized, intentionally excluded, or already absorbed into a design-reference lane.

## Problem Statement

A large batch of Universal Manifest research and design materials exists in `/Users/grig/Downloads/INBOX-markdown/`, but the current state is mixed. Some of the materials were already localized during earlier K2B work, some were already absorbed into design reference folders, and some remained only in the inbox. Without a fresh dedupe/import sweep, the project risks duplicate ingestion, stale source uncertainty, and source material stranded outside the repo.

## Scope

In scope:

- Audit the user-supplied Universal Manifest inbox paths and classify each item.
- Confirm which markdown research sources are already represented in the repo knowledge-corpus pipeline.
- Localize missing markdown sources into the internal provenance system.
- Import missing design-reference assets into the appropriate design lane.
- Produce a human-readable crosswalk explaining every disposition.
- Archive the processed inbox materials into `universal-manifest-imported-into-project`.

Out of scope:

- Rewriting the substance of previously integrated reports.
- Promoting newly imported research notes into normative spec text.
- Production site design changes beyond reference-material ingestion.

## Deliverables

1. Formal disposition and crosswalk report:
   - `docs/reports/2026-03-06-universal-manifest-inbox-import-crosswalk.md`
2. New localized import notes for previously unlocalized text sources:
   - `.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`
   - `.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`
   - `.dev/ai/knowledge-corpus/imports/external-27-peermesh-universal-manifest-vision.md`
   - `.dev/ai/knowledge-corpus/imports/external-28-hot-grid-manifest-note.md`
3. Design-reference localization for logo exploration assets:
   - `docs/design/LOGO-REFERENCE.md`
   - `docs/design/logo-reference/`
4. Provenance and selection updates:
   - `.dev/ai/knowledge-corpus/SOURCE-MAP.md`
   - `.dev/ai/ingestion/LEDGER.md`
   - `.dev/ai/knowledge-index/SOURCE-SELECTION.md`
   - `.dev/ai/knowledge-index/CANDIDATE-SOURCES.md`
5. Inbox archive destination:
   - `/Users/grig/Downloads/INBOX-markdown/universal-manifest-imported-into-project/`

## Acceptance Criteria

- [x] Every user-supplied inbox item is classified as already localized, newly localized, already absorbed, or intentionally excluded.
- [x] No previously localized source is duplicated into a second internal lane.
- [x] All newly localized markdown sources follow the existing import-note provenance format.
- [x] Logo exploration assets are copied into a documented design-reference directory.
- [x] Processed inbox sources are moved into the imported archive directory.
- [x] Work-order and status documents reflect the new import wave.

## Execution Progress (2026-03-06)

Started in this pass:

- Audited the explicitly supplied inbox items plus the `universal-manifest/` directory contents.
- Verified earlier localization work through:
  - `.dev/ai/knowledge-corpus/SOURCE-MAP.md`
  - `.dev/ai/ingestion/LEDGER.md`
  - `.dev/ai/knowledge-index/SOURCE-SELECTION.md`
- Confirmed that the cinematic render pack was already absorbed into the design-reference lane.
- Identified four missing markdown sources and one missing logo-reference asset pack requiring new localization.

Completed in this pass:

- Added four new localized import notes for previously untracked inbox markdown sources:
  - `.dev/ai/knowledge-corpus/imports/external-25-user-centric-pointer-protocols-2025-landscape.md`
  - `.dev/ai/knowledge-corpus/imports/external-26-universal-manifest-architectures-comprehensive-analysis.md`
  - `.dev/ai/knowledge-corpus/imports/external-27-peermesh-universal-manifest-vision.md`
  - `.dev/ai/knowledge-corpus/imports/external-28-hot-grid-manifest-note.md`
- Added a design-reference lane for the logo exploration pack:
  - `docs/design/LOGO-REFERENCE.md`
  - `docs/design/logo-reference/`
- Produced the full crosswalk/disposition report:
  - `docs/reports/2026-03-06-universal-manifest-inbox-import-crosswalk.md`
- Synchronized the provenance/indexing system:
  - `.dev/ai/knowledge-corpus/SOURCE-MAP.md`
  - `.dev/ai/ingestion/LEDGER.md`
  - `.dev/ai/knowledge-index/SOURCE-SELECTION.md`
  - `.dev/ai/knowledge-index/CANDIDATE-SOURCES.md`
- Archived the processed inbox material under:
  - `/Users/grig/Downloads/INBOX-markdown/universal-manifest-imported-into-project/`

## Dependencies

- `docs/workorders/WO-0016-gas-index-scan-and-knowledge-integration-ledger.md`
- `docs/workorders/WO-0017-corpus-to-ia-and-journey-synthesis.md`
- `.dev/ai/knowledge-corpus/SOURCE-MAP.md`
- `.dev/ai/ingestion/LEDGER.md`
- `docs/design/CAPSULE-POD-DESIGN.md`

## Completion notes

- The earlier K2B corpus remained the authoritative location for already localized markdown sources.
- WO-0129 closed the remaining gaps without creating a second competing research-import lane.
- The inbox source materials are now archived outside the repo in one dedicated imported-project directory.
