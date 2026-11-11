---
inclusion: auto
name: ui-design-language
description: UI design language for the Quartz garden (tokens, type roles, component patterns, CSS override rules). Read before any styling, theme, font, colour or layout change.
---

# UI design language

The look is the Flexoki theme with a custom type system (Mackinac headings, light Bricolage text) and navy/gray light-mode inks layered on top.

## Where styling lives

| Concern | File |
|---|---|
| Theme, palette for generated assets (og images), font variables | `quartz.config.yaml` (`@quartz-themes/core` flexoki, `quartz-fonts`, `configuration.theme`) |
| Font loading (`<link>` tags) | `quartz/components/Head.tsx` |
| Every visual override | `quartz/styles/custom.scss` |

Do not add other style files. `configuration.theme.typography` must name Google fonts (og-image fetches them), so it keeps Fraunces as header; the site itself never shows Fraunces.

## Principles

1. **Weight and size follow the text's role**, not one weight everywhere (see Type roles).
2. **Tokens, not literals.** Colours come from the `--ink-*` / callout / accent variables. Add a variable before adding a new colour.
3. **Mobile-first.** Plain value for phones, then step up at `$bp-sm` / `$bp-lg`.
4. **Override the theme by specificity, never `!important`** (the only `!important` is the reduced-motion reset).
5. **Light mode uses navy/gray inks; dark mode uses Flexoki tones in the same light-to-dark order.**

## Tokens

### Colour

| Token | Light | Dark | Use |
|---|---|---|---|
| `--ink-strong` | `#191034` | `#f2f0e5` | h2–h6, bold, inline code text |
| `--ink` | `#22183c` | `#e6e4d9` | title, lead, links, bullets, breadcrumbs |
| `--ink-text` | `#4c4e67` | `#b7b5ac` | body text |
| `--ink-muted` | `#676b89` | `#878580` | footer, secondary text |
| `--ink-faint` | `#9698b6` | `#6f6e69` | uppercase labels (date, reading time) |
| `--ink-caption` | `#73739c` | `#878580` | figcaptions |
| `--ink-violet` | `#7c3aed` | `#a699d0` | link hover |
| `--callout-text` / `-border` / `-shadow` | violet-tinted rgba | | callout card |
| `--inline-code-bg` | `rgba(231,230,244,.4)` | `rgba(166,153,208,.12)` | inline code |
| `--secondary` | cyan-600 `#24837b` | cyan-400 `#3aa99f` | tag pills, selection, graph |
| `--tertiary` | orange-600 `#bc5215` | orange-400 `#da702c` | tag pill hover |
| `--color-accent`, `-1`, `-2` | cyan 600/500/400 | cyan 400/300/200 | theme accents |
| `--light`, `--lightgray` | Flexoki paper / base-100 | black / base-900 | page and card surfaces, hairlines |

- Accents must stay **plain hex**. The theme's `hsl(calc(...))` breaks Mermaid and the graph.
- Translucent variants use `color-mix(in srgb, <token> N%, transparent)`: 30% underlines, 25% scrollbar thumb and selection, 12% pill fill, 18% pill hover.
- Code blocks are dark in both modes: `#121226` background, `#fff` text, Shiki `--shiki-dark` token colours (vitesse-dark).
- Light mode also maps the tokens onto theme/Quartz variables (`--dark`, `--darkgray`, `--text-*`, `--bold-color`, `--h*-color`). Dark mode does not (see Open inconsistencies).

### Fonts

| Variable | Family | Use |
|---|---|---|
| `--mackinac` (`--titleFont`, `--headerFont`, `--h*-font`) | P22 Mackinac Pro (Adobe kit `pso3wdg`) | page title, all headings |
| `--bodyFont` (also `--font-interface`) | Bricolage Grotesque, variable `opsz,wdth,wght` | everything else |
| `--codeFont` | `ui-monospace, SFMono-Regular, "Fragment Mono", Menlo, monospace` | code |

Global settings on `body`: `font-variation-settings: "opsz" 24` (reset to `normal` on code), `-webkit-font-smoothing: antialiased`, `text-wrap: wrap`.

### Weights

| Weight | Role |
|---|---|
| 325 | reading text (body, lists, callout text, code) |
| 450 | UI text (sidebar, explorer, breadcrumbs, captions, tag pills); `--nav-item-weight` |
| 500 | headings (Mackinac), lead, bold, callout titles |
| 575 | small uppercase labels |

Italics inherit weight. Nothing in the design uses 600 or more; the theme's base `a` weight of 600 is overridden wherever it shows.

### Width (`font-stretch`)

98.5% body/reading text, 98% UI text, bold, lead, captions, callout titles, 97.5% uppercase labels.

### Type scale

| Role | < 640px | ≥ 640px | Line height | Tracking |
|---|---|---|---|---|
| Article title | 30px | 36px, 44px at ≥ 1024px | 1.25 | -0.025em / word +0.025em |
| h2 | 24px | 30px | 1.325 | -0.025em / word +0.025em |
| h3 | 20.5px | 24px | 1.6 → 1.325 | same |
| h4 | 20.5px | 20.5px | 1.325 | same |
| h5, h6 | 18px | 18px | 1.325 | same |
| Lead | 20.5px | 20.5px | 1.6 | -0.025em |
| Body, lists | 16px | 19px | 1.625 → 1.6 | normal |
| Callout text, code block | 16px | 16px | 1.5 / 1.6 | normal |
| Breadcrumbs | 14.5px | 14.5px | | |
| Labels, captions, footer | 12px | 12px | 1.6 | labels +0.05em uppercase |
| Inline code, tag pills | 0.9em / 0.85em | | | |

Headings: tracking is negative, word-spacing gives it back. Page title uses -0.03em.

### Spacing (rem)

| Value | Use |
|---|---|
| 0.2em | list item gap, list pulled up toward the paragraph above (-0.2em) |
| 0.75 | under the article title, under callout titles |
| 1.25 | paragraph/list bottom margin |
| 1.5 | popover padding, gap between breadcrumbs and title |
| 0.75 | under headings |
| 2 | padding of code blocks |
| 1.25 / 1.5 | padding of callouts (vertical / horizontal) |
| 1.75 / 2 | above / below tables (on `.table-container`) |
| 2.5 | above/below code blocks and callouts |
| 2.5 → 3 (≥ 640px) | above headings; 0 when first child |

### Layout

- Breakpoints: `$bp-sm: (min-width: 640px)`, `$bp-lg: (min-width: 1024px)`. Use these, not Quartz's 800px variables, for anything typographic.
- Text column: `max-width: 44rem` on `p, ul, ol, blockquote, .lead`.
- Code blocks, callouts and tables also stay inside the 44rem column (`pre` uses `box-sizing: border-box`). Letting them stick out collides with the left sidebar.

### Shape and elevation

| Radius | Use |
|---|---|
| 16px | callouts, code blocks |
| 14px | popover card |
| 12px | images, video, Mermaid, tables |
| 999px | tag pills, scrollbar thumb |

| Shadow | Use |
|---|---|
| `0 10px 15px -3px, 0 4px 6px -4px` in `--callout-shadow` | callouts |
| `0 8px 30px -12px rgb(0 0 0 / .25)` | images |
| `0 20px 50px -20px rgb(0 0 0 / .35)` + `backdrop-filter: blur(14px)` | popovers |

### Motion

`transition: <prop> 0.2s ease` (links only so far). Everything is disabled under `prefers-reduced-motion`.

## Component patterns

- **Links** (`a.internal-link`, `a.external`): `--ink`, 1px underline at 30%, offset 2px, weight inherit, no background. Hover: `--ink-violet`, underline 30% violet.
- **Tag pills** (`a.internal.tag-link`; not `.internal-link`): `--secondary` text on 12% fill, 999px radius, padding `0.15rem 0.65rem`, 0.85em, 450. Hover: `--tertiary` on 18% fill. Colours are set via local `--pill-*` vars.
- **Bullets**: `•` drawn with `::before` at `left: -1.25em` in `--ink`; lists indent 1.25em with `box-sizing: border-box`. Task lists keep native markers.
- **Callout card**: `--light` surface, 1px `--callout-border`, 16px radius, callout shadow, `1.25rem 1.5rem` padding, 2.5rem vertical margin, 0.75rem between blocks, none under the last. Title in Bricolage 16px/500; keeps the theme's per-type icon and title colour.
- **Lead**: opt-in only, via `> [!lead]` callout (all card styling stripped, title hidden) or `<div class="lead">`. Never applied automatically.
- **Code block**: dark card, 16px radius, 2rem padding, 2.5rem margin. Mermaid blocks (`pre:has(> code.mermaid)`) are excluded. The `<pre>` scrolls sideways, not the inner `<code>` (`overflow: visible`), so the scrollbar sits at the card's bottom edge. Thin thumb in white at 25% on a transparent track, inset 16px from the corners.
- **Inline code**: `--codeFont` 0.9em/325, `--ink-strong` on `--inline-code-bg`, 2px vertical padding, no radius or border.
- **Content meta** (date, reading time): the uppercase label role.
- **Popover**: frosted card (see shape table), 1.5rem padding, thin ink scrollbar (`scrollbar-color` plus `::-webkit-scrollbar` for Safari), title 2rem.
- **Note lists** (`.section-li > .section`): date and title on a shared baseline, `column-gap: 1rem`, h3 margin 0.
- **Selection**: `--secondary` at 25%.

## Override conventions

| To beat | Use |
|---|---|
| Theme variables on `:root:root[saved-theme]` | `:root:root:root[saved-theme]` (or `[saved-theme="light"/"dark"]`) |
| Theme text rules (`html[saved-theme] body p`, `body a.internal-link`) | `:root[saved-theme] body article …` |
| Theme callout rules | `:root:root[saved-theme] body article .callout` |
| Popover overrides of page rules | `:root:root:root[saved-theme] body .popover …` |

- Note content is inside `article .markdown-rendered`; direct-child rules need `article .markdown-rendered > …`.
- Popovers render the target page's `.popover-hint` elements, so any page-level layout rule (margins, bleed, widths) must be checked and, if needed, reset under `.popover`.
- Give every section in `custom.scss` a `// ── Name ──` header and a one-line reason for any non-obvious rule.

## Open inconsistencies

Candidates for standardising. Decide before relying on them.

1. **Two accent families.** Links and hover use ink/violet. Tags, selection, graph and theme accents use Flexoki cyan/orange.
2. **Dark-mode variable mapping.** Only light mode maps `--dark`, `--darkgray`, `--text-*`, `--bold-color` and `--h*-color` to ink tokens. In dark mode, page chrome uses the theme/config values (`darkgray #CECDC3` vs `--ink-text #b7b5ac`).
3. **Radii.** 16 / 14 / 12px with no rule for which applies. Could collapse to a card radius and a media radius as tokens.
4. **Shadows.** Three recipes; images and popovers use raw black instead of a token.
5. **Hairline borders.** The popover uses `--lightgray`, callouts use `--callout-border`.
6. **Code-block colours** `#121226` / `#fff` are literals, not tokens.
7. **h4 at 20.5px and h5/h6 at 18px** extend the scale without a step-up at 640px like h2/h3.

## Planned roles

Not built yet. Use these values when they're needed so they fit the system:
- Sidenote: 14.5px, 325, 98.5%, line height 1.6, `--ink-muted`, 240px wide in the right margin on desktop.
- Author block and next/previous links: 17px, 450, 98%, `--ink`.
