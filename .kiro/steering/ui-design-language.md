---
inclusion: auto
name: ui-design-language
description: UI design language for the Quartz garden (tokens, type roles, component patterns, CSS override rules). Read before any styling, theme, font, colour or layout change.
---

# UI design language

Flexoki theme surfaces, a custom type system (Mackinac headings, light Bricolage text), navy/gray inks and a single purple accent. Everything below is implemented in `quartz/styles/custom.scss`; keep the two in sync.

## Where styling lives

| Concern | File |
|---|---|
| Theme, font variables, palette for generated assets (og images) | `quartz.config.yaml` (`@quartz-themes/core` flexoki, `quartz-fonts`, `configuration.theme`) |
| Font loading (`<link>` tags) | `quartz/components/Head.tsx` |
| Tokens and every visual override | `quartz/styles/custom.scss` |

- Do not add other style files.
- `configuration.theme.colors` mirrors the tokens (`dark` = `--ink`, `darkgray` = `--ink-text`, `secondary` = `--accent`, `tertiary` = `--accent-strong`, `highlight` = `--highlight`). Change both together.
- `configuration.theme.typography` must name Google fonts (og-image fetches them), so it keeps Fraunces as header; the site never shows Fraunces.

## Principles

1. **Weight and size follow the text's role** (see Type).
2. **Tokens, not literals.** Components use only the tokens below. Add a token before adding a new colour, radius, shadow or blur. Literals are allowed only inside token definitions and as `none`/`0` resets.
3. **One accent: purple.** Links (hover), tags, selection, explorer, graph and theme accents all use `--accent`. Callout types keep the theme's own icon colours; `==highlight==` marks keep the config's yellow `textHighlight`.
4. **Mobile-first.** Plain value for phones, then step up at `$bp-sm` / `$bp-lg`.
5. **Override the theme by specificity, never `!important`** (only the reduced-motion reset uses it).
6. **Both modes share one mapping.** Only raw token values differ per mode; light uses navy/gray inks, dark uses Flexoki base tones in the same order.

## Tokens

### Colour (per mode)

| Token | Light | Dark | Use |
|---|---|---|---|
| `--ink-strong` | `#191034` | `#f2f0e5` | h2–h6, bold, inline code |
| `--ink` | `#22183c` | `#e6e4d9` | title, lead, links, bullets, breadcrumbs, overlay controls |
| `--ink-text` | `#4c4e67` | `#b7b5ac` | body text, page chrome |
| `--ink-muted` | `#676b89` | `#878580` | footer, hints |
| `--ink-faint` | `#9698b6` | `#6f6e69` | uppercase labels |
| `--ink-caption` | `#73739c` | `#878580` | figcaptions |
| `--accent` | `#7c3aed` | `#a699d0` | the accent |
| `--accent-strong` | `#6d28d9` | `#c4b9e0` | accent hover |
| `--accent-1`, `--accent-2` | `#8b5cf6`, `#a78bfa` | `#8b7ec8`, `#c4b9e0` | theme accent variants |
| `--highlight` | accent 10% | accent 12% | theme highlight (rgba; the graph reads it) |
| `--line` | `rgba(91,33,182,.12)` | `rgba(166,153,208,.18)` | card and panel borders |
| `--shadow-tint` | `rgba(91,33,182,.075)` | `rgba(0,0,0,.3)` | tint inside card/overlay shadows |
| `--callout-text` | `rgba(40,25,80,.7)` | `rgba(230,228,217,.75)` | callout body |
| `--inline-code-bg` | `rgba(231,230,244,.4)` | `rgba(166,153,208,.12)` | inline code |

Theme/Quartz variables mapped from these in both modes: `--color-accent*`, `--secondary` (accent), `--tertiary` (accent-strong), `--dark`, `--darkgray`, `--text-normal/-muted/-faint`, `--bold-color`, `--inline-title-color`, `--h1-color`…`--h6-color`. Surfaces `--light` / `--lightgray` come from the theme.

Accents must be plain hex or rgba: the theme's `hsl(calc(...))` breaks Mermaid and the graph, and so would `color-mix` in variables the graph reads.

### Colour (mode-independent)

| Token | Value | Use |
|---|---|---|
| `--line-subtle` | ink 10% | dividers inside a card |
| `--hover-fill` | ink 7% | hovered rows |
| `--scrollbar` | ink 25% | scrollbar thumb everywhere |
| `--code-bg`, `--code-text` | `#121226`, `#fff` | code blocks (dark in both modes) |
| `--code-scrollbar` | white 25% | code block scrollbar |
| `--backdrop` | `rgb(0 0 0 / .3)` | page dimming behind search and the graph |

Inline translucency uses `color-mix(in srgb, <token> N%, transparent)`: 30% link underline, 25% selection, 12% tag fill, 18% tag hover fill.

### Shape, elevation, blur

| Token | Value | Use |
|---|---|---|
| `--radius-card` | 16px | callouts, code blocks, popovers, search panel, graph box |
| `--radius-media` | 12px | images, video, Mermaid, tables |
| `--radius-inner` | 8px | rows inside a card (card radius minus 8px padding) |
| `--radius-pill` | 999px | tags, close button, hint, scrollbar thumb |
| `--shadow-card` | `0 10px 15px -3px`, `0 4px 6px -4px` in tint | callouts |
| `--shadow-media` | `0 8px 30px -12px` black 25% | images |
| `--shadow-overlay` | `0 30px 60px -20px` black 35% + `0 10px 20px -10px` tint | popovers, search panel, graph box |
| `--blur` | 12px | popover card and both backdrops |

Borders are always `1px solid var(--line)`.

### Fonts

| Variable | Family | Use |
|---|---|---|
| `--mackinac` (`--titleFont`, `--headerFont`, `--h*-font`) | P22 Mackinac Pro (Adobe kit `pso3wdg`) | page title, all headings |
| `--bodyFont` (also `--font-interface`) | Bricolage Grotesque, variable `opsz,wdth,wght` | everything else |
| `--codeFont` | `ui-monospace, SFMono-Regular, "Fragment Mono", Menlo, monospace` | code |

On `body`: `font-variation-settings: "opsz" 24` (`normal` on code), `-webkit-font-smoothing: antialiased`, `text-wrap: wrap`.

### Weights and width

| Weight | Stretch | Role |
|---|---|---|
| 325 | 98.5% | reading text: body, lists, callout text, code |
| 450 | 98% | UI text: sidebar, explorer, breadcrumbs, captions, tags, search input, hints (`--nav-item-weight`) |
| 500 | 98% | Mackinac headings and titles, lead, bold, callout titles |
| 575 | 97.5% | small uppercase labels |

Italics inherit weight. Nothing uses 400 or 600+.

### Type scale

| Role | < 640px | ≥ 640px | Line height |
|---|---|---|---|
| Article title | 30px | 36px; 44px at ≥ 1024px | 1.25 |
| h2 | 24px | 30px | 1.325 |
| h3 | 20.5px | 24px | 1.325 |
| h4 | 18px | 20.5px | 1.325 |
| h5, h6 | 16px | 19px | 1.325 |
| Lead | 20.5px | 20.5px | 1.6 |
| Body, lists, search input | 16px | 19px | 1.625 → 1.6 |
| Callout text, callout title, code block, search result title | 16px | 16px | 1.5 (callout), 1.6 (code) |
| Breadcrumbs | 14.5px | 14.5px | |
| Labels, captions, footer, hints | 12px | 12px | 1.6 |
| Inline code / tags | 0.9em / 0.85em | | |

- Popover title uses 30px. The graph's "×" glyph uses 24px.
- All Mackinac text (page title, article title, headings) uses `letter-spacing: -0.025em` with `word-spacing: 0.025em`. Lead: -0.025em. Labels: +0.05em uppercase. Bold: -0.005em.

### Spacing

| Value | Use |
|---|---|
| 0.2em | list item gap; lists pulled up by -0.2em |
| 0.75rem | under article title, headings and callout titles; between blocks in a callout |
| 1rem | under breadcrumbs; date–title gap in note lists |
| 1.25rem | under paragraphs, lists and the lead |
| 1.25 × 1.5rem | callout padding |
| 1.5rem | popover padding |
| 2rem | code block padding |
| 1.75 / 2rem | above / below tables |
| 2.5rem | above/below code blocks and callouts |
| 2.5 → 3rem (≥ 640px) | above headings; 0 when first child |

### Layout

- Breakpoints: `$bp-sm` = 640px, `$bp-lg` = 1024px. Use these for typography, not Quartz's 800px variables (`$mobile` is only used for overlay positioning).
- Column: `max-width: 44rem` for paragraphs, lists, blockquotes, lead, code blocks, callouts and tables. Nothing sticks out of it (that collides with the sidebar). `pre` uses `box-sizing: border-box`.

### Motion

`transition: <prop> 0.2s ease` (links). Everything is disabled under `prefers-reduced-motion`.

## Component patterns

- **Links** (`a.internal-link`, `a.external`): `--ink`, 1px underline at 30%, offset 2px, weight inherit, no background. Hover: `--accent`, underline accent 30%.
- **Tag pills** (`a.internal.tag-link`; not `.internal-link`): set through the theme's `--pill-*` vars. `--accent` on 12% fill; hover `--accent-strong` on 18%. `--radius-pill`, padding `0.15rem 0.65rem`, 0.85em, 450. The theme's pill on the wrapping `ul.tags > li` is removed.
- **Bullets**: `•` via `::before` at `left: -1.25em` in `--ink`; 1.25em indent, `box-sizing: border-box`. Task lists keep native markers.
- **Callout card**: `--light`, border, `--radius-card`, `--shadow-card`, `1.25rem 1.5rem` padding, 2.5rem margin. Title Bricolage 16px/500 with the theme's per-type icon colour. No margin under the last block.
- **Lead**: opt-in only, via `> [!lead]` (card styling stripped, title hidden) or `<div class="lead">`.
- **Code block**: `--code-bg`/`--code-text`, `--radius-card`, 2rem padding, Shiki `--shiki-dark` tokens. `pre` (not the inner `code`) scrolls horizontally; it sets `--scrollbar: var(--code-scrollbar)` and insets the track by the card radius. Mermaid blocks are excluded.
- **Inline code**: `--codeFont` 0.9em/325, `--ink-strong` on `--inline-code-bg`, 2px vertical padding, no radius or border.
- **Media**: `--radius-media`; images also get `--shadow-media`.
- **Content meta** (date, reading time): the uppercase label role in `--ink-faint`.
- **Scrollbars**: one global style for every scroller (page, sidebars, explorer, TOC, backlinks, search, popovers, tables, code). Thin, transparent track, `--scrollbar` thumb with `--radius-pill`, inset 2px by a transparent border with `background-clip: padding-box`; 8px in WebKit. Components never restyle scrollbars; they only override `--scrollbar`.
- **Overlay card** (popover, search panel, graph box): `--light`, border, `--radius-card`, `--shadow-overlay`. Popover is frosted (`blur(var(--blur))`), 1.5rem padding.
- **Overlay backdrop** (search, graph): `--backdrop` + `blur(var(--blur))`.
- **Search**: input and results form one panel; the input is its top row (19px/450, `--ink`), separated by `--line-subtle`. Results are 8px-padded with `--radius-inner` rows that take `--hover-fill` on hover/focus. Preview padding `1.5rem 2rem`.
- **Graph overlay**: "×" close button (2rem circle, `--light`, border) and a keyboard hint pill (12px/450, `--ink-muted`) sit on the backdrop; clicking outside the box closes it.
- **Note lists** (`.section-li > .section`): date and title on a shared baseline, h3 margin 0.
- **Selection**: accent 25%.

## Override conventions

| To beat | Use |
|---|---|
| Theme variables on `:root:root[saved-theme]` | `:root:root:root[saved-theme]` (or `[saved-theme="light"/"dark"]`) |
| Theme text rules (`html[saved-theme] body p`, `body a.internal-link`) | `:root[saved-theme] body article …` |
| Theme callout rules | `:root:root[saved-theme] body article .callout` |
| Theme search, graph, tag `li` rules | `:root:root:root[saved-theme] body …` |

- Note content is inside `article .markdown-rendered`; direct-child rules need `article .markdown-rendered > …`.
- Popovers render the target page's `.popover-hint` elements, so page-level layout rules also apply inside the 30rem preview. Check them there.
- Each section in `custom.scss` gets a `// ── Name ──` header and a one-line reason for any non-obvious rule.

## Planned roles

Not built yet. Use these values when needed:
- Sidenote: 14.5px, 325, 98.5%, line height 1.6, `--ink-muted`, 240px wide in the right margin on desktop.
- Author block and next/previous links: 17px, 450, 98%, `--ink`, links `--accent`.
