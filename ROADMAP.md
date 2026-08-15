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
| **1.4** | **More data formats** — JSONL/NDJSON per-record view, plus `.geojson`, `.har`, `.webmanifest`, `.ipynb`, and lock-file recognition; print / save as PDF. |
| **1.5–1.6** | **Built for scale** — multi-gigabyte logs and datasets open in seconds, streamed from disk; search, zoom, and colour stay responsive at 10 GB; many reading-polish rounds. |
| **1.7** | **A window of its own** — theme-matched custom title bar, document controls in the reading column, reorganized File menu; **signed MSI + NSIS installers**, verified down to the binaries inside them. |
| **1.8** | **Trustworthy at the edges** — per-type file icons in the navigator; charts paint full-size at narrow widths; dense files decide their colouring up front (no flash-then-drop); hive-safe uninstall; the app stands in Windows' **Open-with** list for every format it reads (1.8.1). |

## Next up

- **AI review & refinement.** A read-only document assistant that can outline, summarize, check
  links, and review a document — and later propose refinements as **reviewable diffs** you approve
  or reject. Same confinement rules as the reader: the assistant sees only the open folder.

## Under consideration

Roughly in the order we're thinking about them — nothing here is scheduled.

- **More data formats in the viewer** — `jsonc`/`json5` (comment-tolerant) and `csv`/`tsv`
  (simple table view), under the same offline, non-executing contract. (`jsonl`/`ndjson` shipped
  in 1.4.)
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
- The two packages serve different needs and should never share a machine: the **MSI** installs
  per-machine and carries the Explorer Preview Pane; the **NSIS setup** installs just for you with
  no elevation and no preview pane. Setup exes older than 1.7.6 are withdrawn; replace them via
  the MSI or the Store rather than running their uninstaller.
- Versioning is semantic: patch releases fix and polish, minor releases add capability.
