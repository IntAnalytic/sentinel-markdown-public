<div align="center">

# sentinel-markdown

**A fast, private Markdown reader that stays locked to the folder you open.**

Renders a folder of Markdown the way VS Code's preview does — tables, Mermaid diagrams,
live charts, math — but **confined to that folder**: no access elsewhere on disk, and **no network**
in the render path. Safe to point at anything.

[![Get it from the Microsoft Store](https://img.shields.io/badge/Microsoft%20Store-Get%20the%20app-0067b8?logo=microsoft&logoColor=white)](https://apps.microsoft.com/detail/xpfcktgcf2f8dz)
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
- 🧩 **Data viewer** — `json` / `jsonl` / `ndjson` / `yaml` / `toml` / `txt` files (plus
  `.geojson`, `.har`, `.webmanifest`, `.ipynb`, `Cargo.lock`, `poetry.lock`) and data-shaped code
  fences render with a **Pretty ⟷ Raw** toggle. All parsing is offline and non-executing.
- 🐘 **Built for scale** — multi-gigabyte logs and datasets open in seconds and scroll smoothly,
  streamed from disk rather than loaded whole.
- 🔗 **Wiki-links & backlinks** — `[[Name]]`-style links resolve within the folder, with a
  backlinks panel.
- 🔎 **Search** — in-document find plus folder-wide full-text search.
- 🗂️ **Folder navigator** — recursive tree with per-type file icons, recents, and live updates as
  the folder changes on disk.
- 🧭 **Made to read** — document outline with scroll-spy, source ↔ render split with synced
  scrolling, back/forward history, light/dark themes, whole-UI zoom.
- 🖨️ **Export & print** — print or save any document as a PDF, or export it as a single,
  script-free, self-contained HTML file.
- 🔒 **Confined & sanitized** — the app reads only the open folder and its subfolders; all rendered
  HTML/SVG is allowlist-sanitized under a strict CSP; no scripts run, no remote fetches,
  **no telemetry**.
- 🖥️ **Windows integration** — opens by double-click as the `.md` handler, stands in the
  **"Open with" list for every format it reads** (your existing defaults are never touched), and
  registers the **Explorer Preview Pane** for Markdown (MSI installs).

## Install

**[Microsoft Store](https://apps.microsoft.com/detail/xpfcktgcf2f8dz)** (recommended):
one-click install with automatic updates.

**Direct download.** Signed installers for the newest version are on the
[**Releases**](../../releases) page (also mirrored at
[iasols.io](https://www.iasols.io/downloads/)), with release notes. Two packages, and they are
**not interchangeable — install one, never both**:

| Package | Scope | Admin? | Explorer Preview Pane | Pick it when |
|---|---|---|---|---|
| **MSI installer** | per-machine (`Program Files`) | yes | **yes** | you want the preview pane |
| **Setup exe (NSIS)** | just for you, no elevation | no | no | you cannot elevate |

Both register the `.md` association; the machine-wide Open-with entries for data types come with
the MSI. Setup exes older than 1.7.6 have been withdrawn — if you have one installed, update via
the MSI or the Store rather than running the old uninstaller.

## Writing Markdown that renders well

Diagrams, charts, math, and SVG all live **inside** the document as declarative blocks — no
scripts. What renders: GFM, ` ```mermaid ` fences, ` ```chart ` / ` ```vega-lite ` JSON fences,
KaTeX math (`$$…$$`), and inline or relatively-referenced SVG. What is deliberately stripped for
safety: raw HTML/JS, `<script>` tags, remote images, and anything that would need the network.
Blocks that can't run render harmlessly as code.

### Teach your AI to write for this reader

If you generate Markdown with an AI assistant, install the **`markdown-visuals`** agent skill. It
tells the assistant which primitives this reader renders — so you get a Mermaid diagram or a
`chart` block instead of a Chart.js widget that gets stripped.

It follows the open [Agent Skills](https://agentskills.io) format, so it works in Claude Code,
Claude Cowork, and any other agent that supports the standard.

- 📦 **[Download the skill](../../raw/main/skills/markdown-visuals.zip)** (ZIP) · browse the source
  in [`skills/markdown-visuals/`](skills/markdown-visuals/SKILL.md)

**Claude Cowork, or the Claude desktop and web apps** — upload the ZIP as-is; don't unzip it:

1. Open **Customize** in the left sidebar, then the **Skills** tab.
2. Click **+**, then **Create skill → Upload a skill**.
3. Select `markdown-visuals.zip`.

**Claude Code** — unzip so the `markdown-visuals` folder lands in a skills directory:

| Scope | Location |
|---|---|
| Every project (personal) | `~/.claude/skills/markdown-visuals/` |
| One project only | `<project>/.claude/skills/markdown-visuals/` |

On Windows, `~` is `C:\Users\<you>`. A running session picks the skill up immediately; restart only
if you had to create the `skills` directory itself. Claude applies it on its own when writing
Markdown, and you can invoke it directly with `/markdown-visuals`. From a shell:

```bash
curl -L -o markdown-visuals.zip https://github.com/IntAnalytic/sentinel-markdown-public/raw/main/skills/markdown-visuals.zip && unzip markdown-visuals.zip -d ~/.claude/skills/
```

**Any other AI tool** — the same guidance is a paste-ready prompt block in
[`AUTHORING-FOR-AI.md`](skills/markdown-visuals/references/AUTHORING-FOR-AI.md); drop it into your
system prompt or custom instructions.

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
