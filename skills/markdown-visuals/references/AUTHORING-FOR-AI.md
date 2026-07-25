# Authoring Markdown for sentinel-markdown

A capabilities brief for **any AI or tool that generates Markdown to be read in
sentinel-markdown**. It lists the rich primitives the reader renders — and, just as
importantly, what it refuses — so output targets the right building blocks instead of
HTML/JS widgets that get stripped.

> Paste the **"Instruction block"** below into a system/developer prompt. The rest of this
> file explains the *why*. (The same brief ships as an agent skill — the
> [`markdown-visuals`](../SKILL.md) skill this file is bundled with.)

---

## Instruction block (paste this)

```
You are writing Markdown that will be rendered in sentinel-markdown, a folder-confined reader.
Build visuals using ONLY the declarative, data-in-the-document primitives below. The renderer
sanitizes all output and runs NO scripts, so interactive HTML/JS (Chart.js, D3, <canvas>,
<script>, onclick, iframes) will not execute — express every visual as Markdown, a Mermaid
diagram, a chart spec, or inline/relative SVG.

WHAT RENDERS
- CommonMark + GitHub-Flavored Markdown: headings, **bold**/*italic*, lists, task lists
  (`- [ ]` / `- [x]`), blockquotes, rules, links, footnotes, strikethrough, and tables with
  column alignment. Headings get stable anchor ids (outline + `[x](#heading)` links work).
- Relative links between docs (`./other.md`, `../dir/x.md`) navigate within the folder; a
  `#heading` suffix scrolls to that heading in the target.
- Wiki-links for intra-folder cross-references: `[[Name]]`, `[[Name|Label]]`, `[[Name#Heading]]`,
  `[[path/to/Name]]`. They resolve to a markdown file in the folder and navigate like a relative
  link; an unresolved target renders as an inert styled span. A **Backlinks** panel lists the docs
  that reference the open one.
- YAML front-matter at the very top: flat `key: value` pairs are parsed; `title:` shows as a
  document header. (Not full YAML — keep it flat.)
- Math via KaTeX: inline **and** display both use double-dollar — `$$E = mc^2$$`. A single `$`
  is treated as a literal dollar sign (so currency like `$100`/`$2,000` renders normally).
- Syntax-highlighted code: fenced blocks with a language tag (```ts, ```python, ```json, …),
  shown with a copy button. Unknown/absent language → plain monospace.

MERMAID — fence with `mermaid` (flowchart, sequence, gantt, class, state, …). Keep labels short;
it inherits the light/dark theme:
  ```mermaid
  flowchart LR
    A[Open doc] --> B{In root?}
    B -- yes --> C[Render]
    B -- no  --> D[New jailed window]
  ```

CHARTS (data-driven, two options; data MUST be inline — no remote URLs):
1) `chart` — compact JSON shorthand (compiles to Vega-Lite):
   type = "bar"|"line"|"area"|"point"; data = inline rows; x, y = field name or
   {"field","type":"quantitative|nominal|ordinal|temporal"}; optional series (color); optional title.
   ```chart
   { "type": "bar", "title": "FP per day",
     "data": [ {"day":"Mon","fp":28}, {"day":"Tue","fp":209}, {"day":"Wed","fp":49} ],
     "x": "day", "y": "fp" }
   ```
2) `vega-lite` — full Vega-Lite v5 spec for richer charts (arc/pie, layered, faceted):
   ```vega-lite
   { "data": { "values": [ {"phase":"Docs","n":6}, {"phase":"AI","n":8} ] },
     "mark": {"type":"arc","tooltip":true},
     "encoding": { "theta": {"field":"n","type":"quantitative"},
                   "color": {"field":"phase","type":"nominal"} } }
   ```

IMAGES / SVG
- Reference LOCAL images with relative paths only: `![Alt](charts/fig.svg)` — .svg/.png/.jpg/.gif/.webp,
  inside the opened folder (no `..` escaping the root). Remote (http/https) images are blocked.
- Inline `<svg>…</svg>` is allowed (sanitized). Use theme-safe colors or `currentColor` so it works
  in light AND dark mode; add `<title>`/`<desc>` for accessibility.

DO NOT (stripped or blocked)
- No `<script>`, `on*` handlers, `javascript:` URLs, `<iframe>/<object>/<embed>/<style>`, remote
  `<script src>`. No Chart.js/D3/canvas — use `chart`/`vega-lite`/`mermaid`.
- No network: all data and assets are local/inline.
- Always give images `alt` text and use a correct heading hierarchy (the DOM is read by screen
  readers and by the AI reviewer).

FORMATTING HYGIENE
- Write plain Markdown — do NOT backslash-escape `#`, `-`, `*`, `[`, `]`.
- GFM tables: header, `|---|` separator, then data rows on CONSECUTIVE lines (a blank line between
  rows breaks the table). Don't double-space the document.
```

---

## Why these are the boundaries

sentinel-markdown is a **folder-confined reader of untrusted documents** — point it at any folder
and it must stay safe. So:

- **Sanitizer + CSP (ADR-0003 / FR-31).** All rendered HTML/SVG passes an allowlist and a strict
  Content-Security-Policy (`script-src 'self'`, no `unsafe-eval`). `<script>`, event handlers, and
  remote/inline scripts never run. Charts work under this strict CSP because Vega uses its **AST
  expression interpreter** (no `eval`) — so `chart`/`vega-lite`/`mermaid` are safe *and* render.
- **No network in the render path (FR-4).** Remote images and chart `data.url` are refused — every
  visual carries its own data/source inline.
- **Confinement (ADR-0004).** Images and linked docs resolve only inside the opened folder.

Live HTML/JS widgets (Chart.js, D3, interactive `<canvas>`) are a deliberate **research topic, not a
feature** — tracked on the [roadmap](https://github.com/IntAnalytic/sentinel-markdown-public/blob/main/ROADMAP.md).
Today such blocks render as code; use the declarative primitives above instead.

This brief is also the authoring contract for the planned **AI reviewer**, which should emit exactly
these primitives when proposing content.
