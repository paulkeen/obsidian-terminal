# Changelog

All notable changes to Terminal. This file is the engineering record; the
[README](README.md) is the user-facing description.

## 2.1.0

Green dark read as a wall of green on black. Measured, that was two separate
problems.

Every text tier was saturated green: body `#9ce8ac` at 62% saturation, with
fg-bright only 1.12x its luminance. Nearly every lit pixel carried the
phosphor hue, so headings, links and bold had nothing to stand out against.
And the three grounds sat 1.03 to 1.09:1 apart, below what the eye separates,
so note, sidebar and code block merged into one black field.

Changes, green dark only:

1. Body text is a green-cast neutral, `#c9d6cf` (14% saturation, 12.5:1).
   Muted `#8ea69b` (7.2:1) and faint `#62786f` (3.95:1) follow it. Saturated
   green, `#62f5a0`, is now reserved for headings, links, cursor and the
   active item. The file tree goes neutral as a side effect.
2. The ground is a cool slate at about 197° instead of near-black, and the
   sidebars now sit darker than the note (`#0a0e10` vs `#0e1315`), with
   raised surfaces at `#162024`. Adjacent surfaces are 1.13 to 1.17:1 apart.
3. Bold is "bright white", `#e8f2ec` (16.3:1), as ANSI terminals render it,
   via a new `--term-fg-bold` variable.
4. Bloom is limited to h1 and the inline title. h2, h3, links and bold use a
   new `--term-glow-minor`, which green dark sets to `transparent`.

Both new variables default to the old behaviour, so amber, cyan, paper-white
and all light palettes render exactly as before. Every tier was checked
against bg, bg-alt and bg-raised and clears the 7 / 4.5 / 3 floors.

## 2.0.2

The caret after the note title was `\2588` FULL BLOCK at `0.78em` of the title,
so on the green palette it was ~19px of `#5cff9e` (plus the `terminal-glow`
bloom, which reaches a pseudo-element because `text-shadow` inherits) switching
between opacity 1 and 0 every 1.1s. Too much lit area next to the text to be
flashing.

It is an underscore now. Same `--term-fg-bright`, same bloom, same hard
`steps(1)` 1.1s switch, a fraction of the ink. The `0.78em` override went with
the block: the title face is monospace, so at 1em the underscore is exactly one
cell wide, where a terminal would put the cursor.

## 2.0.1

File names in the file explorer sat about 2ch right of the folder names beside
them, so a run of files under a folder read as that folder's children. Cause:
the leaf bullet was inline content on `.nav-file-title-content`, and the two
characters it added were laid out in the row. Obsidian's own collapse arrow is
`position: absolute` in the gutter and costs the row nothing, which is why
folders and files line up in vanilla.

The bullet is now hung off the row itself in that same gutter: a
`var(--size-4-4)` box at `calc(-1 * var(--size-4-5))`, with a matching positive
end margin so the three margins net to zero. File names land on their sibling
folders' names exactly, and the bullets land in the arrow column. Row height
and baselines are untouched.

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
