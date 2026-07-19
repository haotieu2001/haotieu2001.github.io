# haotieu2001.github.io — Design & Content Conventions

Personal site of **Hao Tieu Kim** (Tieu Kim Hao) — Data Engineer. Static site on
GitHub Pages (no build step, plain HTML/CSS/JS, `.nojekyll`). The home page
(`index.html`) is the canonical "terminal-dashboard" look; `blogs.html`,
`essentials.html` and every article follow it.

## Deploy / repo rules
- GitHub Pages serves the **`main`** branch root. Push to `main` to go live.
- Commit author MUST be `Hao Tieu <haotieu1601@gmail.com>` (maps to GitHub
  `haotieu2001`). Never commit with any other email.
- Never commit large binaries or a `.claude/` worktree gitlink — they break the
  Pages build. `.claude/` is gitignored; keep it that way.
- Display name is **"Hao Tieu Kim"** everywhere (title, hero, nav wordmark,
  footer). GitHub handle `haotieu2001` and email `haotieu1601@gmail.com` are NOT
  renamed.

## Design system — the "terminal-dashboard" theme

### Tokens (CSS `:root`)
```
--bg:#111117;  --bg2:#16161d;  --panel:#191921;  --line:#2c2c38;
--ink:#F1F1F1; --soft:#cdd0dd; --muted:#9aa0b4; --dim:#6b6b78;
--cyan:#28B9FF; --cyan2:#5AC8FF;   /* PRIMARY accent */
--blue:#5C78FF;                    /* single SUPPORT accent */
--grad2:linear-gradient(90deg,#28B9FF,#5C78FF);   /* the only gradient: 2-stop, cool */
--font:"JetBrains Mono", ui-monospace, monospace;
/* 8-pt spacing scale */ --s1:8 --s2:16 --s3:24 --s4:32 --s5:48 --s6:64 --s7:96 (px)
```
Canvas is a soft near-black (`#111117`), never pure black. Off-white text
(`--soft` body, `--muted` secondary, `--dim` captions).

### Colour — restrained, validated 2026
- **One PRIMARY + one SUPPORT only.** Primary = **cyan** (`--cyan`/`--cyan2`):
  links, active nav, section/tab numbers, hover borders, code, key figures, glow.
  Support = **blue** `#5C78FF` for secondary / alternating elements. **No third
  brand hue.** (Benchmark: Chiang / Linear / Stripe / Vercel ≈ 1 accent; >3 hues
  reads busy/junior.)
- **The display name renders SOLID cyan** (`#5AC8FF`) — hero `h1` and nav
  wordmark. NOT a gradient.
- **Gradient = `--grad2` only** (2-stop cyan→blue). Use it *only* on: the hero
  `.herobar`, the scroll-progress `#bar`, and the primary button. Never on
  headings, cards, dividers, or as a rainbow.
- **Amber / magenta / red are FUNCTIONAL only** — a warning box (`.pain` = amber),
  an error, a highlighted metric — where the hue carries meaning. Never
  decorative, never cycled per section.
- **Two-tier rule (important):**
  - **UI / chrome** (nav, panels, cards, callouts, `.pain`/`.fix`, `.tldr`,
    badges, headings, text) stays on cyan + blue (+ functional amber/red).
  - **Diagrams** (inline SVG + `.diagram` ASCII) MAY use the fuller **neon
    palette** — cyan `#5AC8FF`, blue `#5C78FF`, purple `#A56BFF`, magenta
    `#FF6B9D`, amber `#FFB454` — **but only when colour encodes distinct
    information** (series / categories / layers). One-thing diagram = cyan.
    Brand logos (AWS, Docker, Git, Spark…) and the Medallion bronze/silver/gold
    keep their real colours. Diagram text must never match the shape behind it
    (no hidden text) and must stay inside the viewBox (no clipping).

### Signature components
- **Sticky blurred top nav** on every page: cyan wordmark **HAO TIEU KIM** left;
  tabs right — `Portfolio` (index.html) · `Blogs` (blogs.html) · `Data Engineer
  Essentials` (essentials.html). From a subfolder prefix links with `../`; mark
  the current tab `.active`. `#bar` scroll-progress uses `--grad2`.
- **Dashboard panel** = the home motif: `.panel` = `--panel` bg, `1px` accent
  border, `14px` radius, soft accent glow (`box-shadow:0 0 34px -16px <accent>`),
  with a corner-label **tab** floating on the top-left border — a glowing dot +
  `NN` number + label (e.g. "01 About"). Home sections and the blogs/essentials
  card grids use this; panel accents alternate cyan/blue (identity from the
  number label, not the hue).
- **Cards:** `--bg2` bg, `1px --line`, hover `translateY(-4px)` + cyan border +
  soft cyan glow. Pill tags. `.reveal` fade-up via IntersectionObserver.
- **8-pt spacing**, generous whitespace, `line-height` 1.7–1.85.

### No icon glyphs / emoji
No checkmarks, crosses or emoji as icons (✓ ✗ ✅ ❌ 📚 📋 ☁ ⚡ ⚙ …). Use text /
typographic marks: `+` / `−` for has/lacks, `~` partial, `·`/`—` bullets, word
labels. Keep only the terminal prompt `❯`, the `∎` end mark, and arrows
`→ ← ↑ ↓`.

### Accessibility
Real semantic tags; `:focus-visible{outline:2px solid var(--cyan2)}`;
`@media (prefers-reduced-motion:reduce)` disables animation + smooth scroll.
Body text ≥4.5:1 contrast.

## Blog / article conventions
- Same tokens + colour rules as above (reskin, don't reinvent). Articles are
  long-form prose — do NOT wrap every section in a dashboard panel; keep the
  reading column clean and use the shared palette/accents.
- Structure: sticky nav → hero (kicker `~/path ❯ …`, cyan/`--grad2` `h1`, `.dek`,
  optional `.herobar`) → a `.wrap` of prose. Numbered `h2` with a
  `~/path ❯ label` `.promptline` above it.
- Reusable blocks: `.tldr`, `.callout` (cyan left border; `.mg` = blue support),
  `.pain` (functional amber) / `.fix` (cyan), `.pull`, `.def`, `figure.fig`,
  `.tablewrap`/`table`, `.code` (mono, `--panel` bg, cyan), `details`.
- **Footer (every article):** `← Back to all articles` (→ `../blogs.html` for
  blogs, `../essentials.html` for essentials) then
  `© 2026 · Hao Tieu Kim · Built with GitHub Pages`.
- Diagrams: hand-built inline SVG (sometimes base64), may animate. Follow the
  two-tier colour rule above.
- **Content style:** plain English, example-driven, friendly, "explain from
  zero". Prefer concrete examples, worked scenarios and runnable SQL/PySpark
  over abstraction. Detailed and thorough is good.

## Diagram, text & colour QA — recurring bugs to ALWAYS prevent

These are the error classes already swept site-wide and fixed. Apply them by
default to any new/edited page, diagram or code block — the user should never
have to report them again. When editing, re-run the checks below.

### Neutral surfaces — cool only, no warm leftovers
Every topic page was reskinned from an original accent theme (git=orange,
spark=amber, sql/postgres=red…). Those left **warm-tinted neutral surfaces**
(brownish/olive) that clash with the cool canvas. **All chrome surfaces use the
cool neutrals only:**
```
page bg #111117 · deep #16161d · panel/box bg #191921 · raised #1D1D26
table header #23232c · zebra #1a1a22 · border/line #2c2c38 · code surface #1D1D26
```
- Banned as surfaces: any hex where `r > b` and it's a dark near-neutral
  (e.g. `#171411 #241a15 #241d1a #1a1614 #302823 #2a2622 #231a14 #241014 #221b0e`).
  Snap them to the cool neutrals above.
- Semantic accents stay **clean**, never muddy: `.pain` = neutral `#191921` body
  + solid amber left-bar `#FFB454` (no warm gradient bg); a danger callout uses
  clean **magenta** `#FF5C8A` border + `#FF8FB0` title (on-palette), never grey
  border + brown-red bg.
- Watch for **malformed hex** (e.g. a 9–10 digit `#4a2a1c2f3a`) — invalid CSS;
  fix to a valid 6-digit cool value.

### Text in diagrams — bright, never grey, never hidden
**No grey/dim text anywhere inside an SVG or `.diagram`.** Diagram text is white
`#E7E7EE`/`#fff` on dark shapes, dark `#14141C` on light shapes. Grey hides in
MANY places — check every one:
- inline `fill="#9AA0B4"` / `#6b6b78` etc. on `<text>`;
- 3-digit hex (`#555`, `#888`);
- SVG internal `<style>` class fills (`.sub`, `.comment`, `.h-sub`…);
- `<g fill="#9AA0B4">` inheritance (child `<text>` with no own fill);
- `<text>` with **no fill at all** (inherits a dim default);
- HTML `<figcaption>` colour — must be bright, not `#555`/`#8a90a6`.
- **Opacity-aware contrast:** a fill's *effective* colour = blend(fill, bg,
  opacity). A low-opacity light fill is effectively dark → put light text on it.
  Compute against the effective bg, not the raw hex.
- **No hidden text:** text colour must never equal the shape/line behind it
  (esp. a cyan label on a cyan arrow). Text must stay inside the `viewBox`
  (no clipping at edges).

### Arrows
- **Marker direction:** with `orient="auto"` the marker path must point RIGHT
  (`M0 0 L6 3 L0 6 z` or `M0 0L10 5L0 10z`, tip on the +x side). A down/other
  path double-rotates → arrow points the wrong way. (These right-pointing paths
  ARE correct — don't "fix" them.)
- **Endpoints land ON the box edge** — not overshooting inside the box, not
  stopping short. Clip the segment to the target rectangle's edge.
- **No text/arrow overlap:** a label must not sit on its arrow line (same-colour
  = hidden). Offset the label perpendicular into open space; verify by measuring
  min distance from each `<text>` centre to every path segment (≥ ~6px).
- Arrows drawn *inside* a full-size background `<rect>` are NOT overshoots —
  don't flag those.

### Titles, headings, code
- `h1` (hero) = **solid cyan `#5AC8FF`**, never a running gradient.
- **`h2` is `display:flex`** — an inline element (`<em>`, `<code>`) placed mid-
  title becomes its OWN flex item and the text on each side splits into separate
  items, breaking the line ("… that / are / containers"). **Wrap the entire
  post-icon title text in a single `<span>`** so the whole title is one flex
  item with the inline element flowing inside it. Verify the rendered line isn't
  split. (Affected pages had `<em>are</em>`, `<em>will</em>`.)
- **Code-block command tokens must be bright, not grey.** In `<pre>` syntax
  spans, command/keyword tokens (`.k`) and shell variables (`.p`), plus unused
  `.o/.y/.r`, render **white `#fff`** (were grey `#9AA0B4` and hard to read).
  Keep strings (`.g`) cyan `#5AC8FF` and comments (`.c`) dim `#6B6B78`. SQL
  keyword highlighting may keep its accent colour, but shell/git commands = white.

### How to verify (do this after any diagram/theme edit)
Run quick Python passes over each edited file (decode+re-encode any base64 SVG):
grey text-sources = 0, hidden/low-contrast (opacity-aware) = 0, off-theme/warm
surfaces = 0, malformed hex = 0, markers right-pointing, text→segment distance
≥ ~6px, arrow endpoints on box edges, `h1` solid cyan, figcaptions bright.
Then confirm live: Pages build succeeded and the page returns HTTP 200.
