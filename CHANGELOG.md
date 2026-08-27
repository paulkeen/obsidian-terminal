# Changelog

All notable changes to Terminal. This file is the engineering record; the
[README](README.md) is the user-facing description.

## 2.0.0

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

## 1.0.0

Initial release. Green phosphor on near-black, monospace throughout, full-window
CRT scanlines and vignette, blocking cursor, `#` heading prompts, four phosphor
colours, Style Settings support.
