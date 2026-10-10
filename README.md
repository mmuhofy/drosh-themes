# Drosh Themes

A collection of terminal themes for [Drosh](https://github.com/mmuhofy/drosh), stored in the
Drosh TOML palette format.

Every theme in `themes/` is converted from the
[iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes) `.itermcolors`
plist files, so the palettes are battle-tested and widely used.

**120 themes · dark and light · `index.json` catalogue**

## Installing

### From the Theme Store

Open Drosh and go to **Settings → Appearance → Theme Store**. The store reads this
repository's `index.json`, so every theme listed there is one click away. Pick a theme
to preview and install it; it is saved locally and applied immediately.

### From a URL

Any theme in this repository can be installed directly by URL:

```sh
drosh theme install https://raw.githubusercontent.com/mmuhofy/drosh-themes/main/themes/dracula.toml
```

You can also install from a local file:

```sh
drosh theme install ./themes/dracula.toml
```

List, preview, and switch themes:

```sh
drosh theme list          # installed themes
drosh theme preview nord  # print the palette
drosh theme set nord      # apply a theme
```

## Format

Each theme is a single TOML file with two tables.

### `[meta]`

| Key           | Type   | Description                                                  |
| ------------- | ------ | ------------------------------------------------------------ |
| `id`          | string | Lowercase, dash-separated identifier, e.g. `builtin-dark`.   |
| `name`        | string | Human-readable theme name.                                   |
| `author`      | string | Original theme author, or `iTerm2-Color-Schemes` if unknown. |
| `description` | string | One-line summary of the theme.                               |
| `version`     | int    | Format version. Always `1`.                                  |

### `[palette]`

All colors are `#RRGGBB` in uppercase.

| Key                    | Source                                              |
| ---------------------- | --------------------------------------------------- |
| `background`           | Background Color                                     |
| `foreground`           | Foreground Color                                     |
| `cursor`               | Cursor Color                                         |
| `selection_background` | Selection Color                                      |
| `selection_foreground` | Selected Text Color                                  |
| `accent`               | Ansi 4 Color (blue); falls back to foreground        |
| `black` … `white`      | Ansi 0–7 Color                                       |
| `bright_black` … `bright_white` | Ansi 8–15 Color                              |

### Example

```toml
# Drosh theme — Dracula. Converted from iTerm2-Color-Schemes.
[meta]
id = "dracula"
name = "Dracula"
author = "zenorocha"
description = "A dark purple-tinted theme with vivid pink, green and purple accents."
version = 1

[palette]
background = "#282A36"
foreground = "#F8F8F2"
cursor = "#F8F8F2"
selection_background = "#44475A"
selection_foreground = "#FFFFFF"
accent = "#BD93F9"
black = "#21222C"
red = "#FF5555"
green = "#50FA7B"
yellow = "#F1FA8C"
blue = "#BD93F9"
magenta = "#FF79C6"
cyan = "#8BE9FD"
white = "#F8F8F2"
bright_black = "#6272A4"
bright_red = "#FF6E6E"
bright_green = "#69FF94"
bright_yellow = "#FFFFA5"
bright_blue = "#D6ACFF"
bright_magenta = "#FF92DF"
bright_cyan = "#A4FFFF"
bright_white = "#FFFFFF"
```

## Writing your own theme

1. **Copy a starting point.** Pick a theme close to what you want and copy it:

   ```sh
   cp themes/dracula.toml themes/my-theme.toml
   ```

2. **Update `[meta]`.** Set a unique lowercase `id` matching the filename, your own
   `name`, `author`, and a one-line `description`.

3. **Set the colors.** Edit `[palette]`. Keep all 22 keys present — Drosh reads the full
   set, and omitting one makes the theme invalid. `accent` drives UI highlights, links,
   and the cursor in some contexts; it is usually the same as `blue`.

   When porting from iTerm2, floats are converted with `round(value * 255)`:

   ```python
   '#%02X%02X%02X' % tuple(round(v * 255) for v in (red, green, blue))
   ```

4. **Validate locally.**

   ```sh
   drosh theme preview my-theme
   ```

5. **Share it.** Add an entry to `index.json` (alphabetical by `id`) and open a pull
   request:

   ```json
   { "id": "my-theme", "name": "My Theme", "author": "you",
     "description": "A short one-line description of your theme.",
     "file": "themes/my-theme.toml" }
   ```

### Conventions

- Colors are always uppercase `#RRGGBB`, six digits, no shorthand (`#FFF` is invalid).
- `id` is derived from the filename: lowercase, with spaces and special characters
  replaced by `-` (e.g. `Builtin Dark` → `builtin-dark`).
- Keep `description` to a single short sentence describing the palette's character.

## `index.json`

The catalogue at the repository root. `schema` is the format version, `updated` is the
last modification date, and `themes` lists every theme sorted alphabetically by `id`:

```json
{
  "schema": 1,
  "updated": "2026-10-10",
  "themes": [
    { "id": "dracula", "name": "Dracula", "author": "zenorocha",
      "description": "A dark purple-tinted theme with vivid pink, green and purple accents.",
      "file": "themes/dracula.toml" }
  ]
}
```

## Credits

Palettes converted from
[mbadolato/iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes).
Each theme's original author is credited in its `[meta]` table; individual licenses and
terms still belong to their respective authors.

## License

Released under the [MIT License](LICENSE).
