# Terminal — a retro CRT theme for Obsidian

A dark, green-phosphor, monospace theme that makes your vault look like a 1980s
terminal while keeping all of Obsidian's modern functionality. Built entirely on
Obsidian's native CSS-variable system (the same content-first approach the
Minimal theme popularised), so it stays compatible with core features and
community plugins.

## Features

- **Phosphor green on near-black**, with sharp (zero-radius) corners.
- **Monospace everything** by default; one toggle switches body text back to a
  proportional font if you want easier long-form reading.
- **CRT effects**: horizontal scanlines, a tube vignette, a soft phosphor bloom
  on headings/links, and an optional screen flicker.
- **Block cursor** in the editor that blinks like a real terminal.
- **Heading prompts** (`#`, `##`, …) rendered before reading-view headings, plus
  a blinking block cursor after the note title.
- **Four phosphor colours**: green (P1), amber (P3), cyan, and paper-white
  (VT220). Switchable in one click.
- **Style Settings support** so all of the above are in-app toggles, not
  CSS edits.
- A legible **light-mode "paper printout"** fallback if you flip Obsidian to
  light mode.

## Installation

### Option A — manual (works today, no internet needed)

1. Find your vault's config folder. In Obsidian: **Settings → About** shows the
   vault; the config folder is `<your-vault>/.obsidian/`. (Enable "Show hidden
   files" in your OS file browser, since `.obsidian` starts with a dot.)
2. Create the folder `<your-vault>/.obsidian/themes/Terminal/`.
   > The folder name **must** be exactly `Terminal` — it has to match the
   > `name` field in `manifest.json`.
3. Copy `manifest.json` and `theme.css` from this repo into that folder. You
   should end up with:
   ```
   <your-vault>/.obsidian/themes/Terminal/
   ├── manifest.json
   └── theme.css
   ```
4. In Obsidian go to **Settings → Appearance → Themes** and pick **Terminal**
   from the dropdown.
5. Make sure **Settings → Appearance → Base color scheme** is set to **Dark**
   (the theme is designed dark-first).

#### One-liner if your vault lives at a known path

```bash
# edit VAULT to point at your vault, then run from this repo's folder
VAULT="$HOME/Documents/MyVault"
mkdir -p "$VAULT/.obsidian/themes/Terminal"
cp manifest.json theme.css "$VAULT/.obsidian/themes/Terminal/"
```

After copying, just select the theme in Appearance settings. Edits to
`theme.css` hot-reload on save; if you change `manifest.json` you must restart
Obsidian.

### Option B — unlock the in-app toggles (recommended)

1. Install the **Style Settings** community plugin
   (**Settings → Community plugins → Browse → "Style Settings"**), then enable
   it.
2. A new **Style Settings** entry appears in the settings sidebar. Open it and
   expand **Terminal** to change phosphor colour, scanline intensity, glow,
   fonts, corner radius, and the rest — live, no file editing.

## Customising without Style Settings

Everything is driven by a small set of intermediate variables at the top of
`theme.css` (`--term-bg`, `--term-fg`, `--term-fg-bright`, …). Change those and
the whole theme recolours. To turn an effect off without the plugin, remove the
matching class from the rules in section 8, or just delete that block.

The Style Settings toggles map to these `<body>` classes:

| Toggle               | Class                  | Default |
|----------------------|------------------------|---------|
| Phosphor colour      | `terminal-green` / `-amber` / `-cyan` / `-white` | green |
| CRT scanlines        | `terminal-scanlines`   | on      |
| Phosphor bloom       | `terminal-glow`        | on      |
| Screen flicker       | `terminal-flicker`     | off     |
| Heading prompts      | `terminal-prompts`     | on      |
| Block cursor         | `terminal-block-caret` | on      |
| Proportional body    | `terminal-prop-body`   | off     |

## Notes & limitations

- This is a **standalone theme inspired by Minimal's principles**, not a fork of
  Minimal. It does not read Minimal's own settings; install Style Settings for
  configuration instead.
- The scanline overlay sits above the workspace at a high `z-index` but uses
  `pointer-events: none`, so it never blocks clicks. If you ever see it dimming
  a modal too much, lower **Scanline intensity** or turn scanlines off.
- The phosphor bloom adds a faint blur to body text for authenticity. If you
  find it tiring to read, turn **Phosphor bloom** off — headings/links keep
  their glow only when it's on.
- Tested against the Obsidian 1.5+ variable set. Older versions may miss a few
  variables but will still render.

## Compatibility

Because the theme overrides Obsidian's documented CSS variables rather than
hard-coding element styles, it works with reading view, live preview, the
graph, Canvas, callouts, tables, tasks, and most community plugins out of the
box. Plugins that ship their own colours can be nudged back into the palette by
adding rules that reference `var(--term-fg)` and friends.

## License

Released under the [MIT License](LICENSE).
