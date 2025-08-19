# Tinted8 Styling Guidelines

**Version 0.1.0** The latest version of this spec can be obtained from
[tinted-theming/specs/tinted8/styling](https://github.com/tinted-theming/home/blob/main/specs/tinted8/styling.md)

**Note**: This spec is currently unstable due to development.

Tinted8 aims to make it very simple to style terminal based applications, but can
be heavily expanded to style complex GUI applications. Tinted8 simplifies the
process of creating a color scheme by asking the user to only specify the 8
basic ANSI colors. The builder will then generate all additional colors,
including bright variants, "Black" to "White" gradients, and dim variants.

In this model, the core 8 ANSI colors represent a palette, and the builder
handles the generation of other necessary colors. The design follows a basic
rule where:

- `palette.<black|red|green|yellow|blue|magenta|cyan|white>` are the 8
  user-defined colors.
- Bright and Dim variants of each color are automatically generated.
- `gray` and `brown` colors are automatically generated.

Tinted8 allows scheme authors to style specific theme properties. This is done by
setting override properties and adds a lot of optional flexibility.

## Scheme properties

| Scheme property | Required | Description                                             |
|-----------------|----------|---------------------------------------------------------|
| `system`        | Yes      | Must contain the property value `tinted8`.              |
| `name`          | Yes      | Name of the scheme.                                     |
| `author`        | Yes      | Who authored the scheme?                                |
| `is-dark`       | Yes      | Currently only `dark` and `light` are supported<br> variants. The builder will adjust theme backgrounds<br> and foregrounds based on the `dark` and `light`<br> values here. |
| `variant`       | No       |  Some themse can have different variants, such as <br> "Ayu Dark", "Ayu Light" and "Ayu Mirage". The <br> `variant` property allows users to add `dark`, <br> `light` and `mirage` (in this example) and builders <br> can understand that these are different variants of <br> the same theme. |
| `theme-author`  | No       | Who authored the original theme?                        |
| `palette`       | Yes      | A list of required scheme colors.                       |

### Required scheme `palette` colors

|ANSI Mapping |  Color Name                                                             | Description                           |
|------------ |  ---------------------------------------------------------------------- | ------------------------------------- |
|0            |  palette.black (![#](https://placehold.co/25/282c34/000000?text=%2B))   | Default background color (dark theme) |
|1            |  palette.red (![#](https://placehold.co/25/e06c75/000000?text=%2B))     | error messages                        |
|2            |  palette.green (![#](https://placehold.co/25/98c379/000000?text=%2B))   | Used for strings, success messages    |
|3            |  palette.yellow (![#](https://placehold.co/25/e5c07b/000000?text=%2B))  | Used for constants, warnings          |
|4            |  palette.blue (![#](https://placehold.co/25/61afef/000000?text=%2B))    | Used for functions, method names      |
|5            |  palette.magenta (![#](https://placehold.co/25/c678dd/000000?text=%2B)) | Used for keywords, selectors          |
|6            |  palette.cyan (![#](https://placehold.co/25/56b6c2/000000?text=%2B))    | Used for support, regex patterns      |
|7            |  palette.white (![#](https://placehold.co/25/be5046/000000?text=%2B))   | Used for text and light backgrounds   |

### Optional scheme `palette` colors

| ANSI Mapping | Color Name                                                                    | Description |
| ------------ | ----------------------------------------------------------------------------- | ----------- |
| 8            | palette.black-bright (![#](https://placehold.co/25/282c34/000000?text=%2B))   | n/a         |
| 9            | palette.red-bright (![#](https://placehold.co/25/ff7b86/000000?text=%2B))     | n/a         |
| 10           | palette.green-bright (![#](https://placehold.co/25/b1e18b/000000?text=%2B))   | n/a         |
| 11           | palette.yellow-bright (![#](https://placehold.co/25/efb074/000000?text=%2B))  | n/a         |
| 12           | palette.blue-bright (![#](https://placehold.co/25/67cdff/000000?text=%2B))    | n/a         |
| 13           | palette.magenta-bright (![#](https://placehold.co/25/e48bff/000000?text=%2B)) | n/a         |
| 14           | palette.cyan-bright (![#](https://placehold.co/25/63d4e0/000000?text=%2B))    | n/a         |
| 15           | palette.white-bright (![#](https://placehold.co/25/be5046/000000?text=%2B))   | n/a         |
| n/a          | palette.black-dim (![#](https://placehold.co/25/282c34/000000?text=%2B))      | n/a         |
| n/a          | palette.red-dim (![#](https://placehold.co/25/e06c75/000000?text=%2B))        | n/a         |
| n/a          | palette.green-dim (![#](https://placehold.co/25/98c379/000000?text=%2B))      | n/a         |
| n/a          | palette.yellow-dim (![#](https://placehold.co/25/e5c07b/000000?text=%2B))     | n/a         |
| n/a          | palette.blue-dim (![#](https://placehold.co/25/61afef/000000?text=%2B))       | n/a         |
| n/a          | palette.magenta-dim (![#](https://placehold.co/25/c678dd/000000?text=%2B))    | n/a         |
| n/a          | palette.cyan-dim (![#](https://placehold.co/25/56b6c2/000000?text=%2B))       | n/a         |
| n/a          | palette.white-dim (![#](https://placehold.co/25/be5046/000000?text=%2B))      | n/a         |
| n/a          | palette.gray (![#](https://placehold.co/25/666666/000000?text=%2B))           | n/a         |
| n/a          | palette.gray-bright (![#](https://placehold.co/25/be5046/000000?text=%2B))    | n/a         |
| n/a          | palette.gray-dim (![#](https://placehold.co/25/be5046/000000?text=%2B))       | n/a         |
| n/a          | palette.orange (![#](https://placehold.co/25/d19a66/000000?text=%2B))         | n/a         |
| n/a          | palette.orange-bright (![#](https://placehold.co/25/be5046/000000?text=%2B))  | n/a         |
| n/a          | palette.orange-dim (![#](https://placehold.co/25/be5046/000000?text=%2B))     | n/a         |

### Sample YAML Scheme

Here's what the Tinted8 specification would look like in YAML format:

```yaml
system: "tinted8"
name: "Ayu"
author: "User <user@example.com>"
is-dark: "yes"
variant: "Mirage"
palette:
  black:   "#131721"
  red:     "#f07178"
  green:   "#b8cc52"
  yellow:  "#ffb454"
  blue:    "#59c2ff"
  magenta: "#d2a6ff"
  cyan:    "#95e6cb"
  white:   "#e6e1cf"
```

**Dev Notes**: Thoughts here could be to give the builder access to a dark and
light variant of a theme to allow it to solve things like this:
https://github.com/tinted-theming/tinted-terminal/issues/14

## Optional code Colors

Code templates will largely pull colors from the variables in the table below.
These variables are set by automatically using the `<color>_<variant>` values
generated by the builder, but can be modified directly by the scheme author
using the `override` properties.

**Note**: Have a look at `specs/tinted8/builder.md` for more information about
`<color>_<variant>` values.

| Override Property                   | Default Color   | Description |
| ----------------------------------- | --------------- | ----------- |
| override.comment                    | gray_dim        | Comments in the code, usually for non-executable text providing context or explanation. |
| override.string.quoted              | green_default   | Quoted strings, such as text enclosed in double or single quotes. |
| override.string.regexp              | cyan_default    | Regular expressions, which are patterns used to match character combinations in strings. |
| override.constant.language.boolean  | yellow_bright   | Boolean constants like `true` or `false` in code. |
| override.character.entity           | red_default     | Special character entities, like `&amp;` or `&lt;` in HTML. |
| override.entity.name.class          | yellow_default  | Class names in object-oriented languages. |
| override.entity.name.function       | blue_default    | Function names in code. |
| override.entity.name.tag            | red_default     | hTML or XML tag names, such as `<div>` or `<a>`. |
| override.entity.name.variable       | orange_default  | Variable names in code. |
| override.entity.other.attributeName | yellow_bright   | Attribute names, commonly used in HTML, XML, or other markup languages. |
| override.keyword.control            | magenta_default | Control keywords such as `if`, `else`, `while`, or `for` that define the program's flow. |
| override.keyword.declaration        | magenta_default | Declaration keywords like `let`, `const`, `var`, or `function` used to define variables or functions. |
| override.markup.bold                | yellow_default  | Bold text in markup languages (e.g., `<b>` or `<strong>`). |
| override.markup.code                | green_default   | Inline code or code blocks in markup (e.g., `<code>` or `<pre>` tags). |
| override.markup.italic              | magenta_default | Italic text in markup languages (e.g., `<i>` or `<em>`). |
| override.markup.quote               | cyan_default    | Quoted text in markup languages (e.g., `<blockquote>` or `<q>`). |
| override.diff.added                 | green_bright    | Added lines in a diff view, typically representing new code or content. |
| override.diff.changed               | magenta_bright  | Changed lines in a diff view, typically representing modified content. |
| override.diff.deleted               | red_bright      | Deleted lines in a diff view, typically representing removed code or content. |
| override.ui.background              | black_default   | The general background of the user interface. |
| override.ui.backgroundDark          | black_dim       | Darker background areas, typically used for sidebars, footers, or other sections. |
| override.ui.backgroundLight         | black_bright    | Lighter background areas, typically used for light modes or highlighting. |
| override.ui.deprecated              | brown_default   | Deprecated or outdated UI elements, signaling that they are no longer recommended. |
| override.ui.foreground              | white_default   | General text in the user interface. |
| override.ui.foregroundDark          | gray_bright     | Text in dark-themed UI areas or sections where a lighter font is needed. |
| override.ui.foregroundLight         | white_bright    | Light-colored text in the UI, often used in headings or highlighted sections. |
| override.ui.lineBackground          | gray_dim        | The background of lines in the user interface, such as list items or code lines. |
| override.ui.searchText              | yellow_default  | Text in search results or highlighted search terms. |
| override.ui.selectionBackground     | black_bright    | The background of selected items in the user interface (e.g., highlighted text or options). |

For more information about how these values should be used in templates, have a
look at `specs/tinted8/template.md`.

### Sample YAML scheme

```yaml
system: "tinted8"
name: "Ayu"
author: "User <user@example.com>"
is-dark: "yes"
variant: "dark"

palette:
  black:   "#131721"
  red:     "#f07178"
  green:   "#b8cc52"
  yellow:  "#ffb454"
  blue:    "#59c2ff"
  magenta: "#d2a6ff"
  cyan:    "#95e6cb"
  white:   "#e6e1cf"

override:
  comment: "#555555"
  diff:
    added:   "#00ff00"
    changed: "#0000ff"
    deleted: "#ff0000"
```

_SPEC END_

---
