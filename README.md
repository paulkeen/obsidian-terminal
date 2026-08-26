# Terminal

A monospace theme for Obsidian built around the terminal *interface* rather than
the terminal *photograph*. Box-drawing pane frames, tree glyphs, ruled headings
and a segmented status line, in the spirit of lazygit, btop and ranger. The CRT
effects are still here, but they are scoped to the note surface so they no
longer make the chrome hard to read.

Version 2 is a rebuild. See [Changes in v2](#changes-in-v2).

## Features

### Terminal UI

- **Box-drawing pane frames.** Sidebar panes render as framed boxes with the
  title notched into the top rule. The frame brightens on the focused pane.
- **Tree glyphs.** `▾` / `▸` text triangles instead of rotating SVG chevrons,
  with a dim `·` spine on leaf files.
- **Ruled headings.** Each heading trails a rule to the edge of the column:
  double for `h1`, solid for `h2`, dashed for `h3`.
- **Segmented status line**, with optional Nerd Font powerline separators.
- **Table junctions.** Borders on every cell edge, so intersections read
  as `─┼─`.
- **Optional line-number gutter** in the editor.

### Colour

- **Four phosphors** (green P1, amber P3, cyan, paper-white VT220), each with a
  matching light-mode paper palette. Eight palettes in total.
- **Contrast validated.** Every text tier is measured against the surface it
  actually sits on. Body text clears 7:1 and the muted tier clears 4.5:1 in all
  eight palettes.
- **A high-contrast toggle** for a dimmed laptop panel or a bright room.
- **ANSI-16 semantics** used only where a distinction carries meaning the
  monochrome ramp cannot: callout types, search matches, frontmatter keys, maths,
  unresolved links, errors.

### CRT

- **Additive scanlines** over the note surface only. They lift foreground and
  background together, so they cost under a point of contrast instead of the
  five points the old black-bar overlay cost.
- **Tube vignette** confined to the note pane.
- **Phosphor bloom** on headings, links and accents.
- **Convergence error** (off by default): a sub-pixel red/cyan split on
  headings, like a misaligned electron gun.
- **Phosphor persistence** (on by default): hover and selection colours decay
  instead of snapping.
- **Block cursor**, and a blinking block after the note title.
- **Screen flicker** (off by default).

Everything above is a toggle under **Settings → Style Settings → Terminal**.

## Fonts

The default stack is deliberately not JetBrains Mono, which is the default in
every theme in this genre. Nothing needs installing (the stack falls back), but
the intended pairing is:

| Role | Font | Cost |
|------|------|------|
| Body, code, UI | [Monaspace Neon](https://monaspace.githubnext.com/) | free |
| Headings, pane titles, status line | [Departure Mono](https://www.departuremono.com/) | free, OFL |
| Emphasis | Monaspace Radon | free |

Monaspace's five voices share identical metrics, so mixing them causes no
reflow, and its texture healing fixes the spacing problem monospace body text
normally has. Departure Mono ships box-drawing glyphs, which is why it pairs
with the frames. [Berkeley Mono](https://berkeleygraphics.com/typefaces/berkeley-mono/)
is the paid alternative if you want it.

> **If the fonts do not change:** Obsidian's own **Settings → Appearance →
> Font** fields override the theme. Clear *Interface font* and *Text font* to
> let the theme's stack apply.

## Installation

1. Copy `manifest.json` and `theme.css` into
   `<your-vault>/.obsidian/themes/Terminal/`. The folder name must be exactly
   `Terminal`, matching the `name` in `manifest.json`.
2. Pick **Terminal** in **Settings → Appearance → Themes**.
3. Install the **Style Settings** community plugin to get the toggles.

```bash
VAULT="$HOME/Documents/MyVault"
mkdir -p "$VAULT/.obsidian/themes/Terminal"
cp manifest.json theme.css "$VAULT/.obsidian/themes/Terminal/"
```

`theme.css` hot-reloads on save. Changes to `manifest.json` need a restart.

## Customising without Style Settings

The palette is nine intermediate variables per scheme (`--term-bg`,
`--term-fg`, `--term-fg-dim`, and so on) in section 2. Change those and
everything recolours, including the derived tints, which are computed with
`color-mix` rather than hard-coded.

Section 3 maps those onto Obsidian's semantic variables exactly once, at `body`
scope, so both colour modes get the full theme.

Toggle classes, if you want to hard-set them instead of using the plugin:

| Toggle | Class | Default |
|--------|-------|---------|
| Phosphor | `terminal-green` / `-amber` / `-cyan` / `-white` | green |
| High contrast | `terminal-hicontrast` | off |
| Pane frames | `terminal-frames` | on |
| Tree glyphs | `terminal-tree-glyphs` | on |
| Ruled headings | `terminal-rule-headings` | on |
| Status line | `terminal-statusline` | on |
| Powerline separators | `terminal-powerline` | off |
| Line-number gutter | `terminal-gutter` | off |
| Scanlines | `terminal-scanlines` | on |
| Bloom | `terminal-glow` | on |
| Convergence error | `terminal-aberration` | off |
| Persistence | `terminal-persistence` | on |
| Block cursor | `terminal-block-caret` | on |
| Flicker | `terminal-flicker` | off |
| Proportional body | `terminal-prop-body` | off |

## Changes in v2

The v1 CRT overlay was `position: fixed; inset: 0` at `z-index: 9999`, so it
covered the whole application rather than the note. Measured on the muted text
tier that every sidebar item uses, it cost 2.5x of text luminance and dropped
contrast from 5.94:1 to 3.02:1. The vignette made it worse in one specific
place: with default `farthest-corner` sizing its darkest band falls on the
horizontal extremes, and a right sidebar is a narrow full-height strip sitting
exactly there, so the top and bottom of the outline and backlink lists were the
worst-lit pixels on screen at 2.67:1.

Fixed, in order of how much each recovered:

1. The overlay is scoped to the note pane. It can no longer reach the sidebars,
   and because it now lives inside a workspace leaf it can no longer cover
   modals either.
2. The raster is additive white instead of black bars. Dark bars crush
   foreground and background together but the foreground loses far more
   absolute luminance; light lines lift both.
3. The vignette is confined to the note pane and defaults to `0.12`.
4. The whole ramp moved up off near-black, and the gaps between tiers widened.
5. `--term-fg-faint` no longer shares a value with `--term-border-hi`.
6. A high-contrast toggle.

Also fixed:

- Selecting any phosphor but green used to break light mode entirely, because
  `body.terminal-amber` (0-2-1) outranked a bare `.theme-light` (0-1-0). All
  palettes are now mode-scoped.
- Light mode was missing headings, tags, tables, checkboxes and the entire
  chrome section, all of which were scoped to `.theme-dark`. The mapping layer
  now sits at `body` scope.
- Six hard-coded `rgba(127, 227, 140, …)` values kept hovers, blockquotes,
  table stripes and the active line green under every phosphor. They are
  derived from the palette now.
- Obsidian's base ramp was collapsed (`--color-base-20`/`-25` and `-30`/`-35`
  shared values), removing separation that built-in components rely on.
- Syntax highlighting put functions, variables, class names and operators on
  the dimmest readable tier while numbers got the brightest. Identifiers read
  at body weight now.
- No `prefers-reduced-motion` guard on an indefinitely blinking caret, which is
  a WCAG 2.2.2 problem. The flicker also animated `opacity` on
  `.app-container`, promoting the entire window to a composited layer.
- `--tag-color` and `--tag-background` were set and then contradicted three
  lines later.

Removed: the `#` / `##` heading prompts, which every theme in this genre has.
Ruled headings replace them.

## Compatibility

The theme overrides documented Obsidian CSS variables rather than hard-coding
element styles, so reading view, live preview, graph, Canvas, callouts, tables,
tasks and most community plugins work untouched. Derived tints use `color-mix`,
which needs Chromium 111 or newer; Obsidian 1.5 and above ships well past that.

## License

[MIT](LICENSE).
