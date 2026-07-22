# Roadmap — sentinel-markdown

What has shipped, what's being worked on, and what's under consideration. This is a statement of
direction, not a commitment — priorities shift, and **your feedback moves things**: file a
[feature request](../../issues/new?template=feature_request.yml) or 👍 an existing issue to weigh in.

## Shipped — the 1.x reader

The core reader is feature-complete and shipping on the Microsoft Store and the
[Releases](../../releases) page.

| Version line | Highlights |
|---|---|
| **1.0** | The confined reader: GFM, Mermaid, live charts (Vega-Lite + `chart` shorthand), KaTeX math, SVG; folder navigator; outline + scroll-spy; themes; zoom; sanitized rendering with no network and no telemetry. |
| **1.1** | Folder-wide full-text search, `[[wiki-links]]` + backlinks panel, export as self-contained HTML. |
| **1.2** | Live-updating folder tree, drag-a-file-to-open, sticky "✓ Copied" on code blocks, and a proper dialog for links that point outside the open folder. |
| **1.3** | **Data viewer** — JSON / YAML / TOML / TXT files and data-shaped fences with a Pretty ⟷ Raw toggle; folder search covers data files; source ↔ render scroll-sync fixes; **Windows Explorer Preview Pane** working end-to-end. |

## Next up

- **AI review & refinement.** A read-only document assistant that can outline, summarize, check
  links, and review a document — and later propose refinements as **reviewable diffs** you approve
  or reject. Same confinement rules as the reader: the assistant sees only the open folder.

## Under consideration

Roughly in the order we're thinking about them — nothing here is scheduled.

- **More data formats in the viewer** — `jsonl`/`ndjson` (per-record view), `jsonc`/`json5`
  (comment-tolerant), and `csv`/`tsv` (simple table view), all under the same offline,
  non-executing contract.
- **macOS and Linux builds.** The codebase is cross-platform (Tauri v2); prebuilt, signed binaries
  for macOS and Linux — plus a macOS Quick Look preview extension — are candidates once the
  Windows line is settled.
- **Live interactive widgets** — sandboxed, opt-in execution of embedded HTML/JS widgets
  (Chart.js, D3, …). This conflicts with the current "nothing runs, ever" confinement model, so it
  is a research topic, not a plan. Today such blocks render safely as code, and the declarative
  `chart` / `vega-lite` fences cover the safe slice.

## How releases work

- **Microsoft Store** installs update automatically.
- **Direct downloads** (MSI / NSIS setup exe) are signed and published per release on the
  [Releases](../../releases) page and at [iasols.io](https://www.iasols.io/downloads/); check
  there for new versions.
- Versioning is semantic: patch releases fix and polish, minor releases add capability.
