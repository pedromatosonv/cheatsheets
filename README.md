# cheatsheets

Static HTML cheat sheets. No build step, no dependencies, no JavaScript — open
the files in a browser and they work.

```
index.html        # list of sheets
ghostty.html      # one file per tool, flat at the root
assets/style.css  # shared design system (all sheets use it)
```

Open `index.html` from disk — no server needed. One flat file per tool is the
whole point: the links between pages (`ghostty.html`) are real files, so they
resolve identically over `file://` and over GitHub Pages, and every page reaches
the stylesheet at the same `assets/style.css`. Nested folders would need a server
to turn `ghostty/` into `ghostty/index.html`.

## Publishing

Push to GitHub, then Settings → Pages → deploy from branch `main`, folder `/`.
The sheets land at `<user>.github.io/cheatsheets/` and
`…/cheatsheets/ghostty.html`. Nothing to build.

## Adding to a sheet

**A shortcut** — copy one `<tr>` inside the section's `<tbody>`:

```html
<tr>
  <td class="action">Toggle zoom</td>
  <td class="keys"><kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd></td>
</tr>
```

Conventions:

- Key names, not glyphs, in the abbreviated form: `Cmd`, `Shift`, `Opt`, `Ctrl`,
  `Enter`, `Esc`, `Tab`, `Arrows`.
- One `<kbd>` per key, joined by a literal ` + `. The `+` picks up the muted
  color on its own.
- Keys that are alternatives to each other (a range of digits, for instance) go
  in a `<span class="keygroup">` with no `+` between them — tight spacing reads
  as "any one of these".
- Need a qualifier under the action? `<span class="note">only in fullscreen</span>`.

**A section** — copy a whole `<section>` block, change the `id`, the `<h2>` and
the `<caption>`, then replace the rows. Sections stack in reading order; the
hairline above the first row doubles as the underline for the section label.

## Adding a sheet

1. `cp ghostty.html <tool>.html`
2. Update `<title>`, the masthead, the favicon emoji and the sections.
3. Add one `<li>` to the list in `index.html`, pointing at `<tool>.html`.

`assets/style.css` is shared, so keep tool-specific styling out of it — colors,
type and spacing all come from the custom properties at the top of that file,
and it ships light and dark themes plus a print stylesheet.
