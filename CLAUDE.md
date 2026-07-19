# haotieu2001.github.io — Design & Content Conventions

Personal site of **Hao Tieu (Tieu Kim Hao)** — Data Engineer. Static site on GitHub
Pages (no build step, plain HTML/CSS/JS, `.nojekyll`). The home page
(`index.html`), `blogs.html` and `essentials.html` define the canonical look.
Everything else — especially the blog articles in the topic subfolders — should
follow the conventions below.

## Deploy / repo rules
- GitHub Pages serves the **`main`** branch root. Push to `main` to go live.
- Commit author MUST be `Hao Tieu <haotieu1601@gmail.com>` (maps to GitHub
  `haotieu2001`). Never commit with any other email.
- Never commit large binaries or a `.claude/` worktree gitlink — they break the
  Pages build. `.claude/` is gitignored; keep it that way.

## Design system (the "home" theme)

### Tokens (CSS `:root`)
```
--bg:#191921;  --bg2:#20202a;  --panel:#23232c;  --line:#34343f;
--ink:#F1F1F1; --soft:#cdd0dd;  --muted:#9aa0b4;  --dim:#6b6b78;
/* Canvas is a soft near-black (#191921), NOT pure black — keep it this
   bright or brighter for readability; do not go darker than ~#141419. */
--blue:#5C78FF; --cyan:#28B9FF; --cyan2:#5AC8FF;
--grad:linear-gradient(90deg,#5C78FF,#28B9FF,#A52AFF);
--font:"JetBrains Mono", ui-monospace, monospace;
/* 8-pt spacing scale */ --s1:8 --s2:16 --s3:24 --s4:32 --s5:48 --s6:64 --s7:96 (px)
```

### Rules
- **Font:** JetBrains Mono everywhere (headings, body, code). `line-height` 1.7–1.85.
- **Canvas:** near-black `--bg` background, off-white `--ink`/`--soft` text.
  Body copy uses `--soft` (#cdd0dd); secondary uses `--muted`; captions `--dim`.
- **Accent = one primary + at most one support.** Primary = **cyan**
  (`--cyan` / `--cyan2`) for links, active states, section numbers, card
  borders/hover, code, key figures. A single **cool support** (blue `#5C78FF`)
  may appear for secondary/alternating elements. That's it — no third brand
  hue. (Benchmark: Chiang / Linear / Stripe / Vercel all use ~1 accent; >3
  hues reads busy/junior. Validated 2026.)
- **Amber / magenta / red are functional only** — a warning/highlight metric
  or an error state where the hue *carries meaning*. Never cycle them per
  section as decoration, and never a rainbow gradient.
- **Gradient ≤ 2 stops, same cool family** (e.g. cyan→blue), used at one
  hero moment + the scroll bar — not on every card/heading.
- **Gradient is reserved.** Use `--grad` ONLY for: the `h1` (background-clip text
  with the slow `sheen` animation), the top scroll-progress `#bar`, the primary
  button, and thin dividers/rings. Never gradient body text or many elements.
- **DO NOT use many colours per page.** Purple/magenta/green/red as extra accents
  are out. If several items must be distinguished (e.g. comparing 3 tools), keep
  them all in the **cyan accent** and differentiate with labels/weight, not new
  hues. Blue may appear only as part of the reserved gradient.
- **Spacing:** follow the 8-pt scale. Sections ~96px vertical padding desktop
  (`--s7`), ~64px mobile. Generous whitespace around `h1`.
- **Components (reuse these):** sticky blurred top nav; `#bar` scroll progress;
  cards = `--panel` bg + `1px var(--line)` + 14–16px radius, hover `translateY(-4px)`
  + cyan border + soft cyan shadow; pill tags (`--line` border, `#101018` bg);
  `.reveal` fade-up on scroll via IntersectionObserver.
- **No icon glyphs / emoji.** Do NOT use checkmarks, crosses or emoji as
  icons — ✓ ✗ ✅ ❌ ☑, and pictographs like 📚 📋 ☁ ⚡ ⚙ 🔥 📦. Use plain text
  or restrained typographic marks instead: `+` / `−` for has/lacks, `~` for
  partial, `·` or `—` for bullets, and word labels ("Yes"/"No", "Fix 1 —").
  Card `.strip` labels are plain text (no leading glyph). The only symbols
  kept are the terminal prompt `❯` in kickers/prompt-lines, the `∎` end mark,
  and simple arrows (`→ ← ↑ ↓`). Brand logos (AWS/Databricks/etc.) may keep
  their own colours in diagrams.
- **Accessibility:** real semantic tags; `:focus-visible{outline:2px solid var(--cyan2)}`;
  `@media (prefers-reduced-motion:reduce)` disables animations + smooth scroll.

### Shared top navigation (all pages)
Sticky, blurred, brand `HAO TIEU` on the left, tabs right:
`Portfolio` (index.html) · `Blogs` (blogs.html) · `Data Engineer Essentials`
(essentials.html). From a topic subfolder, prefix links with `../`. Mark the
current page's tab `.active`.

## Blog / article conventions
- Keep the home theme + the "one accent" rule above. Reskin, don't reinvent.
- Structure: sticky nav → centred hero (kicker, gradient `h1`, `.dek`, byline) →
  a `.wrap` (max ~820px) of prose (`.prose`, max ~760px, centred).
- Reusable article blocks: `.tldr` (short version box), `.callout` (left cyan
  border), `.pull` (gradient-edge pull quote), `.def` (definition card),
  `figure.fig` (diagram + italic caption), `.tablewrap`/`table` (striped),
  `.code` (multi-line code block: `--panel` bg, `1px var(--line)`, cyan text),
  `details`/`summary`, numbered `h2` with a `~/path ❯ label` `.promptline` above it.
- Diagrams are hand-built inline SVG (often base64 data URIs) and may animate;
  keep their palette inside the blue–cyan + neutral family only.
- **Content style:** plain English, example-driven, friendly, "explain from zero".
  Prefer concrete examples, small worked scenarios and runnable SQL/PySpark
  snippets over abstract description. Detailed and thorough is good.
