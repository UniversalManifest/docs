# NotebookLM Knowledge Vault — Upload List

**Created:** 2026-03-11
**Updated:** 2026-03-12
**Purpose:** Comprehensive knowledge package for NotebookLM upload.

## Approach: Big Package Zip

Instead of manually uploading individual files (limited to 50 sources), we created a single comprehensive zip archive containing the entire knowledge base. This gives NotebookLM full project context in one upload.

**Zip file:** `notebooklm-knowledge-vault.zip` (project root)

## Package Stats

| Metric | Value |
|---|---|
| Total files | 633 |
| Uncompressed size | ~4.1 MB |
| Compressed size | 1.4 MB |
| Compression ratio | ~66% |

### Breakdown by Directory

| Directory | File count | Description |
|---|---|---|
| `docs/` | 416 | All markdown docs: reports, workorders, scripts, design, journeys, explainers, governance, security, concepts, presentations, research, teaching-scripts, diagrams |
| `examples/` | 115 | JSON/JSONLD fixture files showing real UM data structures |
| `integrations/` | 16 | All integration lane documents |
| `spec/` | 10 | Specification files (README, CONFORMANCE, SIGNATURE-PROFILE, schema.json, context files) |
| Root | 2 | README.md, PROJECT-RULES.md |

## What's Included

- **ALL markdown files from `docs/`** — every subdirectory including reports, workorders, scripts, design, journeys, explainers, governance, security, concepts, presentations, research, teaching-scripts
- **ALL markdown files from `integrations/`** — all 16 integration lane documents
- **ALL files from `spec/`** — both v0.1 and v0.2 specs, schemas, conformance, context files
- **ALL JSON/JSONLD fixtures from `examples/`** — real data structures demonstrating UM envelopes
- **`README.md`** — project overview
- **`PROJECT-RULES.md`** — project-specific rules and configuration

## What's Excluded

- **Binary video files** — `docs/design/capsule-pod-reference/*.mp4` (14.4 MB of reference videos)
- **Binary image files** — `.png`, `.jpg`, `.jpeg`, `.gif`, `.svg`, `.ico`, `.ai` (logos, screenshots)
- **Font files** — `.woff`, `.woff2`, `.ttf`, `.eot`
- **Obsidian config** — `docs/.obsidian/` (editor settings, not knowledge)
- **Excalidraw diagrams** — `.excalidraw` (binary diagram format)
- **AGENTS.md** — operational infrastructure, not UM knowledge
- **`.dev/` directory** — session handoffs, not canonical knowledge
- **Build/runtime artifacts** — `node_modules/`, `dist/`, `.astro/`, `site/`
- **`.git/` directory** — version control internals

## Priority Tiers (Reference)

The original upload list organized files into priority tiers for the 50-source limit. With the zip approach, all tiers are included. For reference, the highest-priority files for focused review remain:

### Tier 1 — Core Understanding
- `README.md` — project overview
- `docs/STATE-OF-THE-PROJECT.md` — current status
- `docs/CRITICAL-PATH.md` — what matters now
- `docs/PROJECT-VISION.md` — long-term direction

### Tier 2 — Specification
- `spec/v0.2/README.md` — current spec
- `spec/v0.2/CONFORMANCE.md` — conformance requirements
- `spec/v0.2/SIGNATURE-PROFILE.md` — signature architecture

### Tier 3 — Architecture
- `docs/ENVELOPE-TOPOLOGY.md` — data model
- `docs/DOMAIN-ARCHITECTURE.md` — system architecture
- `docs/DECISIONS.md` — architectural decisions

### Tier 4 — Positioning and Outreach
- `docs/STANDARDS-POSITIONING.md` — standards landscape
- `docs/MSF-RELATIONSHIP.md` — MSF alignment
- `docs/explainers/full-briefing.md` — comprehensive explainer
- `docs/explainers/agent-briefing.md` — agent-oriented briefing

### Tier 5 — Integration Lanes
- All 16 files in `integrations/` — each covers a specific integration domain

## Notes

- The zip preserves full directory structure for organized extraction
- All content is text-based (markdown, JSON, JSONLD) — no binary content included
- Total text content is ~3.7 MB uncompressed, well within NotebookLM limits
- Work orders are included in full (not just the index), providing complete project history
