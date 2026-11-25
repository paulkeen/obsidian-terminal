<div align="center">

# Terminal

**A TUI theme for Obsidian.** Box-drawing panes, tree glyphs, ruled headings and
a segmented status line, in the spirit of lazygit, btop and ranger. Four
phosphor colours, dark and light. Readable at 2am on a dimmed laptop.

[Install](#install) · [Settings](#settings) · [Fonts](#fonts) · [Changelog](CHANGELOG.md)

</div>

<!-- ────────────────────────────────────────────────────────────────────────
     SCREENSHOTS GO HERE. Drop the files in assets/ and uncomment.
     The community directory also needs assets/screenshot.png at 512x288.

![Terminal](assets/hero.png)

| Green | Amber |
|:--:|:--:|
| ![Green phosphor](assets/green.png) | ![Amber phosphor](assets/amber.png) |
| **Cyan** | **Paper-white** |
| ![Cyan](assets/cyan.png) | ![Paper-white](assets/white.png) |

     ──────────────────────────────────────────────────────────────────────── -->

## Why this one

There are a lot of green-on-black CRT themes. This is not really one of them.

**It looks like a terminal interface, not a photograph of a terminal.** The
retro-computing look that has actually survived is the TUI: framed panes with
titles notched into the border, tree glyphs, segmented status lines, box-drawing
junctions in tables. That is what Terminal is built from. The CRT effects are
here too, but they are seasoning rather than the meal.

**The phosphor is for signal, not for everything.** Body text is a neutral
tinted toward the phosphor's hue, on a lifted slate or charcoal ground rather
than black. The saturated colour is kept for headings, links, the cursor and
the open file, so it reads as emphasis instead of covering every lit pixel.
Bold renders bright white, the way an ANSI terminal renders it.

**It is legible.** Every text colour is measured against the surface it actually
sits on, in all eight palettes. Body text clears 7:1 and muted text clears
4.5:1, so the sidebar is readable with the backlight most of the way down. The
scanlines are additive rather than subtractive, which means they add raster
texture without eating your contrast the way a dark overlay does. There is a
high-contrast toggle for bright rooms.

**It gets out of the way.** Everything is driven through Obsidian's documented
CSS variables rather than hard-coded element styles, so reading view, live
preview, Canvas, graph, callouts and most community plugins work untouched. One
mapping layer serves both colour modes, so light mode is a real theme rather
than an afterthought.

## Features

### Terminal UI

- **Box-drawing pane frames.** Right-sidebar panes render as framed boxes with
  the title notched into the top rule. The frame brightens on the focused pane.
- **Tree glyphs.** `▾` / `▸` text triangles instead of rotating chevrons, with a
  dim `·` spine on files.
- **Reverse-video selection.** The open file in the explorer is a solid
  phosphor bar with dark text, the way ranger and lazygit mark the selected
  row. It does not rely on hue, so it holds up for colour-blind readers.
- **Ruled headings.** Each heading trails a rule to the edge of the column:
  double for `h1`, solid for `h2`, dashed for `h3`. In reading view, Live
  Preview and source mode.
- **Segmented status line**, with optional Nerd Font powerline separators.
- **Box-drawing tables.** Borders on every cell edge, so intersections read
  as `─┼─`.
- **Optional line-number gutter** in the editor.

### Four phosphors, two modes

| | Dark | Light |
|---|---|---|
| **Green** | P1 phosphor on cool slate | dot-matrix printout |
| **Amber** | P3 phosphor on warm charcoal | tractor-feed paper |
| **Cyan** | cold CRT on blue slate | blueprint |
| **Paper-white** | VT220 | plain laser print |

In dark mode the sidebars sit a step darker than the note, a bezel around the
lit screen. Eight palettes, all contrast-validated, including highlighted
text. ANSI-16 colour is used only where a
distinction carries meaning the monochrome ramp cannot: callout types, search
matches, frontmatter keys, maths, unresolved links, errors.

### CRT

- **Additive scanlines** over the note surface only, never the chrome.
- **Tube vignette** confined to the note pane.
- **Phosphor bloom** on the `h1` and the note title only. Bloom only reads as
  bloom when it is rare. Paper-white also blooms `h2`, `h3`, links and bold;
  light mode never blooms.
- **Convergence error** *(off by default)*: a sub-pixel red/cyan split on
  headings, like a misaligned electron gun.
- **Phosphor persistence** *(on by default)*: hover and selection colours decay
  instead of snapping.
- **Block cursor**, and a blinking block after the note title.
- **Screen flicker** *(off by default)*.

Motion respects `prefers-reduced-motion`.

## Install

### From Obsidian

**Settings → Appearance → Themes → Manage**, search for **Terminal**, install,
then select it.

Then install the [Style Settings](https://github.com/mgmeyers/obsidian-style-settings)
plugin to get the toggles. The theme works without it, but Style Settings is
where all the configuration lives.

### Manually

Copy `manifest.json` and `theme.css` into
`<your-vault>/.obsidian/themes/Terminal/`. The folder name must be exactly
`Terminal`, matching the `name` in `manifest.json`.

```bash
VAULT="$HOME/Documents/MyVault"
mkdir -p "$VAULT/.obsidian/themes/Terminal"
cp manifest.json theme.css "$VAULT/.obsidian/themes/Terminal/"
```

`theme.css` hot-reloads on save. Changes to `manifest.json` need a restart.

## Settings

All under **Settings → Style Settings → Terminal**.

| Setting | Default | |
|---|---|---|
| Phosphor colour | Green | green / amber / cyan / paper-white |
| High contrast | off | for a dimmed panel or a bright room |
| Box-drawing pane frames | on | right sidebar |
| Tree glyphs | on | `▾` / `▸` |
| Ruled headings | on | |
| Segmented status line | on | |
| Powerline separators | off | needs a Nerd Font |
| Line-number gutter | off | |
| Scanlines | on | intensity slider |
| Phosphor bloom | on | `h1` and note title |
| Convergence error | off | |
| Phosphor persistence | on | |
| Block cursor | on | |
| Screen flicker | off | |
| Proportional body font | off | keeps UI and code monospace |

Plus sliders for body size, corner radius, scanline intensity and vignette, and
text fields for the two font stacks.

## Fonts

The default stack is deliberately not JetBrains Mono, which is the default in
every theme in this genre. Nothing needs installing, the stack falls back
cleanly, but the intended pairing is:

| Role | Font | |
|---|---|---|
| Body, code, UI | [Monaspace Neon](https://monaspace.githubnext.com/) | free |
| Headings, pane titles, status line | [Departure Mono](https://www.departuremono.com/) | free, OFL |
| Emphasis | Monaspace Radon | free |

Monaspace's five voices share identical metrics, so mixing them causes no
reflow, and its texture healing fixes the spacing problem monospace body text
normally has. Departure Mono ships box-drawing glyphs, which is why it pairs
with the frames. [Berkeley Mono](https://berkeleygraphics.com/typefaces/berkeley-mono/)
is the paid alternative.

> [!TIP]
> **If the fonts do not change:** Obsidian's own **Settings → Appearance →
> Font** fields override the theme. Clear *Interface font* and *Text font* to
> let the theme's stack apply.

## Customising

Each palette is a short block of variables at the top of `theme.css`. Change
those and everything recolours, including the hover, stripe, selection and
highlight tints, which are `color-mix` derivations rather than hard-coded
values.

| Variable | Role | Floor |
|---|---|---|
| `--term-bg` | note surface | |
| `--term-bg-alt` | sidebars, status bar, title bar | |
| `--term-bg-raised` | code blocks, callouts, hovers | |
| `--term-border` / `--term-border-hi` | hairlines / frames and focus rings | |
| `--term-fg` | body text | 7:1 |
| `--term-fg-bright` | headings, links, accents, the selection bar | 4.5:1 |
| `--term-fg-bold` | bold text | 7:1 |
| `--term-fg-dim` | muted text, nav items | 4.5:1 |
| `--term-fg-faint` | faint text, guides | 3:1 |
| `--term-glow` | bloom on `h1` and the note title | |
| `--term-glow-minor` | bloom on `h2`, `h3`, links, bold (`transparent` to turn off) | |
| `--term-highlight-fg` | text colour inside `==highlights==` | 7:1 |

`--term-fg-bold`, `--term-glow-minor` and `--term-highlight-fg` default to
`--term-fg-bright`, `--term-glow` and `--term-fg-bright`, so a palette that
leaves them out gets the all-accent look.

Below that, one mapping layer translates them onto Obsidian's semantic variables
at `body` scope, so both colour modes inherit the whole theme.

Toggle classes, if you would rather hard-set them than use the plugin:

| Toggle | Class |
|---|---|
| Phosphor | `terminal-green` / `-amber` / `-cyan` / `-white` |
| High contrast | `terminal-hicontrast` |
| Pane frames | `terminal-frames` |
| Tree glyphs | `terminal-tree-glyphs` |
| Ruled headings | `terminal-rule-headings` |
| Status line | `terminal-statusline` |
| Powerline separators | `terminal-powerline` |
| Line-number gutter | `terminal-gutter` |
| Scanlines | `terminal-scanlines` |
| Bloom | `terminal-glow` |
| Convergence error | `terminal-aberration` |
| Persistence | `terminal-persistence` |
| Block cursor | `terminal-block-caret` |
| Flicker | `terminal-flicker` |
| Proportional body | `terminal-prop-body` |

## Compatibility

Obsidian 1.5 or newer. Derived tints use `color-mix`, which needs Chromium 111;
Obsidian 1.5 ships well past that.

Because the theme overrides documented CSS variables rather than hard-coding
element styles, reading view, live preview, graph, Canvas, callouts, tables,
tasks and most community plugins work out of the box. Plugins that ship their
own colours can be pulled back into the palette with a snippet referencing
`var(--term-fg)` and friends.

## Contributing

Issues and pull requests are welcome. If you are reporting something visual, a
screenshot and your phosphor / toggle settings help a lot.

If you add or change a colour, check it against the surface it sits on before
opening the PR. The floors the theme holds to are 7:1 for body text, 4.5:1 for
muted text and UI, and 3:1 for faint text and guides.

## Credits

Built on the variable-driven, content-first approach
[Minimal](https://github.com/kepano/obsidian-minimal) popularised. Effect
vocabulary borrowed from [cool-retro-term](https://github.com/Swordfish90/cool-retro-term).
Structural cues from lazygit, btop and ranger.

## License

[MIT](LICENSE).
