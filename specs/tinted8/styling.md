# Tinted8 Styling Guidelines

**Version 0.1.0** The latest version of this spec can be obtained from
[tinted-theming/specs/tinted8/styling](https://github.com/tinted-theming/home/blob/main/specs/tinted8/styling.md)

## Introduction

Tinted8 simplifies the creation of color schemes for terminal and GUI
applications.

This styling specification describes what theme authors should and can provide
through the scheme structure.

The [Builder specification] (a separate document) describes how tools expand
these author-defined values into complete color sets, derive variants and
render template variables.

## Purpose and Scope

This specification is for scheme authors and it defines:

- Which keys appear in a Tinted8 scheme file
- What each key means
- How `syntax` and `ui` inherits

It does **not** define how colors are generated or how files are rendered,
those behaviors belong to the [Builder specification].

## Scheme structure

A Tinted8 scheme is stored as a YAML document with the following fields:

| Property         | Required | Default | Description |
| ---------------- | -------- | ------- | ----------- |
| `system`         | Yes | - | Identifies the spec version used. For Tinted8 schemes this value must be `tinted8`. |
| `system-version` | Yes | - | Identifies the spec version used. For Tinted8 schemes this value must be `tinted8`. |
| `scheme-author`  | Yes | - | The person or organization that created this scheme. |
| `variant`        | Yes | - | Either `dark` or `light`. Indicates the intended luminance direction. The builders will use this to adjust foreground/background balance. |
| `palette`        | Yes | - | Defines the base color palette for the theme. |
| `name`           | No  | Derived from `slug` or `family` + `style` | Human-readable name. |
| `slug`           | No  | Derived from `name` or `family` + `style` | Machine-friendly identifier. |
| `family`         | No  | - | Broad design family (e.g. "Tokyo"). |
| `style`          | No  | - | Variation within a family (e.g. "Night", "Moon"). |
| `theme-author`   | No  | `scheme-author` | Attribution for the original or inspirational theme. |
| `description`    | No  | - | Short human-readable summary. |
| `syntax`         | No  | List of default properties and values available later in this document. | Short human-readable summary. |
| `ui`             | No  | List of default properties and values available later in this document. | Short human-readable summary. |

### YAML scheme example

Here's what the Tinted8 specification would look like in YAML format with all
required properties and some optional properties:

```yaml
system: "tinted8"
scheme-author: "User <user@example.com>"
family: "Ayu"
style: "Mirage"
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
syntax:
  string: "#ffb454"
  entity.name: "#95e6cb"
ui:
  background: "#131721"
```

## Palette Definition

### Required colors

| ANSI Mapping | Example Color | Color Name | Description |
| ------------ | ------------- | ---------- | ------------|
| 0 | ![#](https://placehold.co/25/282c34/000000?text=%2B) | palette.black   | Default background color (dark theme). |
| 1 | ![#](https://placehold.co/25/e06c75/000000?text=%2B) | palette.red     | error messages.                        |
| 2 | ![#](https://placehold.co/25/98c379/000000?text=%2B) | palette.green   | Used for strings, success messages.    |
| 3 | ![#](https://placehold.co/25/e5c07b/000000?text=%2B) | palette.yellow  | Used for constants, warnings.          |
| 4 | ![#](https://placehold.co/25/61afef/000000?text=%2B) | palette.blue    | Used for functions, method names.      |
| 5 | ![#](https://placehold.co/25/c678dd/000000?text=%2B) | palette.magenta | Used for keywords, selectors.          |
| 6 | ![#](https://placehold.co/25/56b6c2/000000?text=%2B) | palette.cyan    | Used for support, regex patterns.      |
| 7 | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.white   | Used for text and light backgrounds.   |

### Optional scheme `palette` colors

| ANSI Mapping | Example Color | Color Name | Description |
| ------------ | ------------- | -----------| ----------- |
| 8   | ![#](https://placehold.co/25/282c34/000000?text=%2B) | palette.black-bright   | n/a |
| 9   | ![#](https://placehold.co/25/ff7b86/000000?text=%2B) | palette.red-bright     | n/a |
| 10  | ![#](https://placehold.co/25/b1e18b/000000?text=%2B) | palette.green-bright   | n/a |
| 11  | ![#](https://placehold.co/25/efb074/000000?text=%2B) | palette.yellow-bright  | n/a |
| 12  | ![#](https://placehold.co/25/67cdff/000000?text=%2B) | palette.blue-bright    | n/a |
| 13  | ![#](https://placehold.co/25/e48bff/000000?text=%2B) | palette.magenta-bright | n/a |
| 14  | ![#](https://placehold.co/25/63d4e0/000000?text=%2B) | palette.cyan-bright    | n/a |
| 15  | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.white-bright   | n/a |
| n/a | ![#](https://placehold.co/25/282c34/000000?text=%2B) | palette.black-dim      | n/a |
| n/a | ![#](https://placehold.co/25/e06c75/000000?text=%2B) | palette.red-dim        | n/a |
| n/a | ![#](https://placehold.co/25/98c379/000000?text=%2B) | palette.green-dim      | n/a |
| n/a | ![#](https://placehold.co/25/e5c07b/000000?text=%2B) | palette.yellow-dim     | n/a |
| n/a | ![#](https://placehold.co/25/61afef/000000?text=%2B) | palette.blue-dim       | n/a |
| n/a | ![#](https://placehold.co/25/c678dd/000000?text=%2B) | palette.magenta-dim    | n/a |
| n/a | ![#](https://placehold.co/25/56b6c2/000000?text=%2B) | palette.cyan-dim       | n/a |
| n/a | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.white-dim      | n/a |
| n/a | ![#](https://placehold.co/25/666666/000000?text=%2B) | palette.gray           | n/a |
| n/a | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.gray-bright    | n/a |
| n/a | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.gray-dim       | n/a |
| n/a | ![#](https://placehold.co/25/d19a66/000000?text=%2B) | palette.orange         | n/a |
| n/a | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.orange-bright  | n/a |
| n/a | ![#](https://placehold.co/25/be5046/000000?text=%2B) | palette.orange-dim     | n/a |

### Generated Colors

Builders will extend these eight required values by generating bright, dim and
neutral variants such as gray, orange and brown. Generation rules are defined
in the [Builder specification].

### Sample YAML Scheme

Here's what the Tinted8 specification would look like in YAML format:

```yaml
system: "tinted8"
scheme-author: "User <user@example.com>"
family: "Ayu"
style: "Mirage"
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
```

## Theming Properties

`syntax` and `ui` properties will be referred to as "Theming Properties".

Scheme authors can refine colors for code elements or UI surfaces using the
Theming Properties. Each key identifies a role with a color reference (hex
color code) value.

| Theming Property                    | Example Context | Purpose |
| ----------------------------------- | --------------- | ------- |
| syntax.comment                      | `// Comment` → `// Comment` | Comments in the code, usually for non-executable text providing context or explanation. |
| syntax.string                       | `"Hello world"` → `"Hello world"` | All string related values. |
| syntax.string.quoted                | `"Hello world"` → `"Hello world"` | Quoted strings, such as text enclosed in double or single quotes. |
| syntax.string.regexp                | `/^Hello/g` → `/^Hello/g` | Regular expressions or patterns used to match character combinations in strings. |
| syntax.string.template              | `` `Hello ${name}` `` → `` `Hello ${name}` `` | Template literals and interpolations. |
| syntax.constant                     | `null` → `null` | Parent of all literal constants (booleans, numbers, nulls, characters, etc.). |
| syntax.constant.numeric             | `42` → `42` | Parent of all numeric constants. |
| syntax.constant.numeric.integer     | `12` → `12` | Integer values. |
| syntax.constant.numeric.float       | `18.1` → `18.1` | Float values. |
| syntax.constant.numeric.hex         | `0x1234ABC` → `0x1234ABC` | Hexadecimal values. |
| syntax.constant.numeric.exponential | `12e3` → `12e3` | Exponential/scientific notation values. |
| syntax.constant.language.boolean    | `true` → `true` | Boolean values. |
| syntax.constant.character           | `'\\n'` → `'\\n'` | Parent of character literal constants (e.g., `'A'`, `'\\n'`, `'\\t'`). |
| syntax.constant.character.escape    | `'What\'s that?'` → `\'` | Escaped characters inside strings. |
| syntax.constant.character.entity    | `Foo&apos;s` → `&apos;` | Special character entities (HTML/XML). |
| syntax.entity.name                  | `class Person {}` → `Person` | Parent of all entity names (class, function, tag, variable). |
| syntax.entity.name.class            | `class Person {}` → `Person` | Class names in object-oriented languages. |
| syntax.entity.name.function         | `function greet() {}` → `greet` | Function names in code. |
| syntax.entity.name.tag              | `<div>Hello</div>` → `div` | HTML or XML tag names. |
| syntax.entity.name.variable         | `let username = "foo";` → `username` | Variable identifiers in code. |
| syntax.entity.other.attribute-name  | `<img src="logo.png">` → `src` | Attribute names, commonly used in HTML, XML, or other markup languages. |
| syntax.keyword                      | `function foo()` → `function` | Language keywords (e.g., function, if, const). Parent of keyword categories. |
| syntax.keyword.control              | `if (x > 0)` → `if` | Control flow keywords. |
| syntax.keyword.declaration          | `const age = 42;` → `const` | Declaration keywords. |
| syntax.markup                       | `<blockquote>Text</blockquote>` → `Text` | Parent of all markup-styled content. |
| syntax.markup.bold                  | `<strong>Foo Bar</strong>` → `Foo Bar` | Bold text. |
| syntax.markup.code                  | `<code>inline</code>` → `inline` | Inline/code blocks. |
| syntax.markup.italic                | `<em>note</em>` → `note` | Italic text. |
| syntax.markup.quote                 | `<blockquote>Be yourself</blockquote>` → `Be yourself` | Quoted text. |
| syntax.diff.added                   | `+ const newFeature = true;` → `+ const newFeature = true;` | Added lines in a diff view, typically representing new code or content. |
| syntax.diff.changed                 | `~ const version = "0.1.0";` → `~ const version = "0.1.0";` | Changed lines in a diff view, typically representing modified content. |
| syntax.diff.deleted                 | `- const oldFeature = false;` → `- const oldFeature = false;` | Deleted lines in a diff view, typically representing removed code or content. |
| ui.background                | Editor canvas → background | The general background of the user interface. |
| ui.background-dark           | Sidebar → background | Darker background areas, typically used for sidebars, footers, or other sections. |
| ui.background-light          | Active tab → background | Lighter background areas, typically used for light modes or highlighting. |
| ui.deprecated                | `<font color="red">Hello</font>` → `<font>` | Deprecated or outdated UI elements, signaling that they are no longer recommended. |
| ui.foreground                | Editor text → `"hello"` | General text in the user interface. |
| ui.foreground-dark           | Sidebar file names → `filename.md` | Text in dark-themed UI areas or sections where a lighter font is needed. |
| ui.foreground-light          | Active tab label → `main.js` | Light-colored text in the UI, often used in headings or highlighted sections. |
| ui.line-background           | Active line highlight → background | The background of lines in the user interface, such as list items or code lines. |
| ui.search-text               | Search results → result | Text in search results or highlighted search terms. |
| ui.selection-background      | Selected code → background | The background of selected items in the user interface (e.g., highlighted text or options). |

The `syntax` properties were largely derived from [TextMate Theme structure].

See the [Builder specification] for the complete canonical list of recognized
Theming Properties as well as the default color values.

## Inheritance

Theming Properties follow a hierarchical fallback system:

1. A specific key (e.g. syntax.constant.numeric.float) inherits from its
   parent (syntax.constant.numeric).
1. If no parent value is provided, it falls back to a builder-defined default
   derived from the palette.

Example rule chain:

```
syntax.string.template → syntax.string → builder default (green_default)
```

This model lets authors define only the Theming Properties they need, builders
ensure the theme remains complete by generating default values for the left out
properties.

## Readable Defaults

Some keys may intentionally default to bright variants (for instance, attribute
names) to preserve legibility in code or markup.

These defaults are suggestions, authors may override them as desired.

## Compliance

A scheme is Tinted8-compliant if it:

- Includes all required fields (`system`, `scheme-author`, `variant`,
  `name|slug|family` `palette`)
- Uses valid color formats (hex `#RRGGBB`)
- Follows the inheritance and structure rules defined here

All further derived or computed colors are implementation details of the
builder.

_SPEC END_

---

[Builder specification]: https://github.com/tinted-theming/home/blob/main/specs/tinted8/builder.md
[TextMate Theme structure]: https://macromates.com/manual/en/language_grammars
