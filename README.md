<div align="center">

# sentinel-markdown

**A fast, private Markdown reader that stays locked to the folder you open.**

Renders a folder of Markdown the way VS Code's preview does — tables, Mermaid diagrams,
live charts, math — but **confined to that folder**: no access elsewhere on disk, and **no network**
in the render path. Safe to point at anything.

[![Get it from the Microsoft Store](https://img.shields.io/badge/Microsoft%20Store-Get%20the%20app-0067b8?logo=microsoft&logoColor=white)](https://apps.microsoft.com/detail/REPLACE-WITH-STORE-PRODUCT-ID)
![platform](https://img.shields.io/badge/platform-Windows-444)
[![license](https://img.shields.io/badge/license-Apache--2.0-green)](LICENSE)

</div>

---

## What this repository is

This is the **public home for sentinel-markdown feedback**: bug reports, feature suggestions,
and the [product roadmap](ROADMAP.md). If you installed the app from the Microsoft Store or a
direct download and something is broken, missing, or could be better — this is the place to say so.

- 🐛 **Found a bug?** [Open a bug report](../../issues/new?template=bug_report.yml)
- 💡 **Have a suggestion?** [Request a feature](../../issues/new?template=feature_request.yml)
- 🗺️ **Wondering what's next?** See the [Roadmap](ROADMAP.md)

Before filing, a quick search of [existing issues](../../issues) helps avoid duplicates — add a 👍
to an existing issue instead; it genuinely influences prioritization.

## What sentinel-markdown does

- 📄 **Full GitHub-Flavored Markdown** — tables, task lists, footnotes, syntax-highlighted code
  with copy buttons.
- 📊 **Diagrams & charts** — [Mermaid](https://mermaid.js.org/) blocks, a compact `chart` JSON
  shorthand, full [Vega-Lite](https://vega.github.io/vega-lite/) specs, and inline/referenced SVG.
- ∑ **Math** — inline and display LaTeX via KaTeX.
- 🧩 **Data viewer** — `json` / `yaml` / `toml` / `txt` files and data-shaped code fences render
  with a **Pretty ⟷ Raw** toggle. All parsing is offline and non-executing.
- 🔗 **Wiki-links & backlinks** — `[[Name]]`-style links resolve within the folder, with a
  backlinks panel.
- 🔎 **Search** — in-document find plus folder-wide full-text search.
- 🗂️ **Folder navigator** — recursive tree, recents, and live updates as the folder changes on disk.
- 🧭 **Made to read** — document outline with scroll-spy, source ↔ render split with synced
  scrolling, back/forward history, light/dark themes, whole-UI zoom.
- 🖨️ **Export & print** — export any document as a single, script-free, self-contained HTML file.
- 🔒 **Confined & sanitized** — the app reads only the open folder and its subfolders; all rendered
  HTML/SVG is allowlist-sanitized under a strict CSP; no scripts run, no remote fetches,
  **no telemetry**.
- 🖥️ **Windows integration** — opens by double-click as the `.md` handler and registers the
  **Explorer Preview Pane** for Markdown.

## Install

**[Microsoft Store](https://apps.microsoft.com/detail/REPLACE-WITH-STORE-PRODUCT-ID)** (recommended):
one-click install with automatic updates.

**Direct download — v1.3.3.** Signed installers; both register the `.md` file association and the
Explorer Preview Pane:

| Package | GitHub | iasols.io |
|---|---|---|
| MSI installer | [Download](../../releases/download/v1.3.3/Sentinel-Markdown_1.3.3_x64_en-US.msi) | [Download](https://www.iasols.io/downloads/Sentinel-Markdown_1.3.3_x64_en-US.msi) |
| Setup exe (NSIS) | [Download](../../releases/download/v1.3.3/Sentinel-Markdown_1.3.3_x64-setup.exe) | [Download](https://www.iasols.io/downloads/Sentinel-Markdown_1.3.3_x64-setup.exe) |

All versions, with release notes, are on the [**Releases**](../../releases) page.

## Writing Markdown that renders well

Diagrams, charts, math, and SVG all live **inside** the document as declarative blocks — no
scripts. What renders: GFM, ` ```mermaid ` fences, ` ```chart ` / ` ```vega-lite ` JSON fences,
KaTeX math (`$$…$$`), and inline or relatively-referenced SVG. What is deliberately stripped for
safety: raw HTML/JS, `<script>` tags, remote images, and anything that would need the network.
Blocks that can't run render harmlessly as code.

## Privacy

sentinel-markdown collects **nothing**. There is no telemetry, no analytics, no network access in
the render path, and no account. Documents never leave your machine.

## Reporting a good bug

The fastest path to a fix is a small Markdown snippet that reproduces the problem, plus your app
version (Help → About), how you installed (Store / MSI / NSIS / standalone exe), and your Windows
version. The bug template walks you through it.

## License

Licensed under the [Apache License, Version 2.0](LICENSE). Copyright © 2026 IAS LLC.

"Sentinel" and the sentinel-markdown name and logos are trademarks of IAS LLC and are not
licensed under Apache-2.0.
