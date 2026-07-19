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
