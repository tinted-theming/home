# Tinted8 Styling Guidelines

**Version 0.2.0-beta4** The latest version of this spec can be obtained from
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

| Property                       | Required | Default | Description |
| ------------------------------ | -------- | ------- | ----------- |
| `scheme.system`                | Yes | - | Identifies the scheme system. For Tinted8 schemes this value must be `tinted8`. |
| `scheme.supports.styling-spec` | Yes | - | Styling spec version implemented by the scheme (e.g. `0.1.0`). |
| `scheme.author`                | Yes | - | The person or organization that created this scheme. |
| `scheme.theme-author`          | No  | `scheme.author` | Attribution for the original or inspirational theme. |
| `scheme.description`           | No  | - | Short human-readable summary. |
| `variant`                      | Yes | - | Either `dark` or `light`. Indicates the intended luminance direction. |
| `scheme.family`                | No  | - | Broad design family (e.g. "Tokyo"). |
| `scheme.style`                 | No  | - | Variation within a family (e.g. "Night", "Moon"). |
| `palette`                      | Yes | - | Defines the base color palette for the theme. |
| `scheme.name`                  | No  | Derived from `slug` or `family` + `style` | Human-readable name. |
| `scheme.slug`                  | No  | Derived from `name` or `family` + `style` | Machine-friendly identifier. |
| `syntax`                       | No  | Defaults documented below | Syntax theming properties. |
| `ui`                           | No  | Defaults documented below | UI theming properties. |

### YAML scheme example

Here's what the Tinted8 specification would look like in YAML format with all
required properties and some optional properties:

```yaml
scheme:
  system: "tinted8"
  supports:
    styling-spec: "0.2.0"
  author: "User <user@example.com>"
  name: "Ayu Mirage"
  slug: "ayu-mirage"
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
  background:
    normal: "#131721"
  foreground:
    normal: "#e6e1cf"
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
| 7 | ![#](https://placehold.co/25/e6e1cf/000000?text=%2B) | palette.white   | Used for text and light backgrounds.   |

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
| 15  | ![#](https://placehold.co/25/fbfaf7/000000?text=%2B) | palette.white-bright   | n/a |
| n/a | ![#](https://placehold.co/25/282c34/000000?text=%2B) | palette.black-dim      | n/a |
| n/a | ![#](https://placehold.co/25/e06c75/000000?text=%2B) | palette.red-dim        | n/a |
| n/a | ![#](https://placehold.co/25/98c379/000000?text=%2B) | palette.green-dim      | n/a |
| n/a | ![#](https://placehold.co/25/e5c07b/000000?text=%2B) | palette.yellow-dim     | n/a |
| n/a | ![#](https://placehold.co/25/61afef/000000?text=%2B) | palette.blue-dim       | n/a |
| n/a | ![#](https://placehold.co/25/c678dd/000000?text=%2B) | palette.magenta-dim    | n/a |
| n/a | ![#](https://placehold.co/25/56b6c2/000000?text=%2B) | palette.cyan-dim       | n/a |
| n/a | ![#](https://placehold.co/25/d3c9a5/000000?text=%2B) | palette.white-dim      | n/a |
| n/a | ![#](https://placehold.co/25/666666/000000?text=%2B) | palette.gray           | n/a |
| n/a | ![#](https://placehold.co/25/8c8c8c/000000?text=%2B) | palette.gray-bright    | n/a |
| n/a | ![#](https://placehold.co/25/4d4d4d/000000?text=%2B) | palette.gray-dim       | n/a |
| n/a | ![#](https://placehold.co/25/d19a66/000000?text=%2B) | palette.orange         | n/a |
| n/a | ![#](https://placehold.co/25/ddb48d/000000?text=%2B) | palette.orange-bright  | n/a |
| n/a | ![#](https://placehold.co/25/bc7939/000000?text=%2B) | palette.orange-dim     | n/a |

### Generated Colors

Builders will extend these eight required values by generating bright, dim and
neutral variants such as gray, orange and brown. Generation rules are defined
in the [Builder specification].

### Sample YAML Scheme

Here's what the Tinted8 specification would look like in YAML format:

```yaml
scheme:
  system: "tinted8"
  supports:
    styling-spec: "0.2.0"
  author: "User <user@example.com>"
  name: "Ayu Mirage"
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
| syntax.comment                      | `// Comment` → `// Comment` | All comment scopes (line, block, documentation). Fallback for unspecified comment types. |
| syntax.comment.line                 | `// Comment` → `// Comment` | Line comments (e.g., `//` or `#` style). |
| syntax.comment.block                | `/* comment */` → `/* comment */` | Block comments (e.g., `/* */` or `"""` style). |
| syntax.comment.documentation        | `/** @param x */` → `/** @param x */` | Documentation comments (e.g., JSDoc, Javadoc, docstrings). |
| syntax.invalid                      | `@` in invalid context → `@` | Invalid or erroneous constructs. |
| syntax.invalid.deprecated           | Deprecated API use → token | Deprecated constructs. |
| syntax.invalid.illegal              | Illegal token → token | Illegal constructs that should not appear. |
| syntax.string                       | `"Hello world"` → `"Hello world"` | All string related values. |
| syntax.string.quoted                | `"Hello world"` → `"Hello world"` | Quoted strings, such as text enclosed in double or single quotes. |
| syntax.string.quoted.single         | `'hello'` → `'hello'` | Single-quoted strings. |
| syntax.string.quoted.double         | `"hello"` → `"hello"` | Double-quoted strings. |
| syntax.string.regexp                | `/^Hello/g` → `/^Hello/g` | Regular expressions or patterns used to match character combinations in strings. |
| syntax.string.template              | `` `Hello ${name}` `` → `` `Hello ${name}` `` | Template literals and interpolations. |
| syntax.string.interpolated          | `` `Hello ${name}` `` → `${name}` | Interpolated/embedded portions inside strings. |
| syntax.string.unquoted              | `hello` → `hello` | Unquoted string content in languages that allow it. |
| syntax.string.other                 | `q{string}` → `q{string}` | Other string types not covered by quoted, regexp, or template. |
| syntax.constant                     | `null` → `null` | All literal constants (booleans, numbers, nulls, characters). Fallback for unspecified constant types. |
| syntax.constant.numeric             | `42` → `42` | All numeric literals. Fallback for integer, float, hex, and exponential numbers. |
| syntax.constant.numeric.integer     | `12` → `12` | Integer values. |
| syntax.constant.numeric.float       | `18.1` → `18.1` | Float values. |
| syntax.constant.numeric.hex         | `0x1234ABC` → `0x1234ABC` | Hexadecimal values. |
| syntax.constant.language            | `true` → `true` | Language-provided constants (e.g., `true`, `false`, `null`, `nil`). |
| syntax.constant.character           | `'\\n'` → `'\\n'` | Character literals and escape sequences. Fallback for escape and entity characters. |
| syntax.constant.character.escape    | `'What\'s that?'` → `\'` | Escaped characters inside strings. |
| syntax.constant.character.entity    | `Foo&apos;s` → `&apos;` | Special character entities (HTML/XML). |
| syntax.constant.other               | `nil` → `nil` | Constants not covered by numeric, language, or character categories (e.g., symbols, atoms). |
| syntax.entity                       | `class Person {}` → `Person` | All named constructs (classes, functions, tags, variables). Fallback for entity scopes. |
| syntax.entity.name                  | `class Person {}` → `Person` | All entity names. Fallback for class, function, tag, type, and variable names. |
| syntax.entity.name.class            | `class Person {}` → `Person` | Class names in object-oriented languages. |
| syntax.entity.name.function         | `function greet() {}` → `greet` | Function names in code. |
| syntax.entity.name.function.constructor | `new Foo()` → `Foo` | Constructor method names. (Non-standard) |
| syntax.entity.name.label            | `loop: for` → `loop` | Labels for goto targets or loop identifiers. |
| syntax.entity.name.tag              | `<div>Hello</div>` → `div` | HTML or XML tag names. |
| syntax.entity.name.type             | `List<String>` → `List` | Type names. |
| syntax.entity.name.type.class       | `class Person {}` → `Person` | Type names for classes. (Non-standard) |
| syntax.entity.name.type.enum        | `enum Status {}` → `Status` | Type names for enums. (Non-standard) |
| syntax.entity.name.namespace        | `MyApp.Utils.foo` → `MyApp` | Namespace/package/module names. |
| syntax.entity.name.section          | Markdown heading → `Heading` | Section or heading names. |
| syntax.entity.other                 | `<img src="logo.png">` → `src` | Miscellaneous entity data. Fallback for attributes and inherited classes. |
| syntax.entity.other.attribute-name  | `<img src="logo.png">` → `src` | Attribute names, commonly used in HTML, XML, or other markup languages. |
| syntax.entity.other.inherited-class | `class B extends A` → `A` | Inherited/extended class names. |
| syntax.keyword                      | `function foo()` → `function` | All language keywords. Fallback for control, declaration, and operator keywords. |
| syntax.keyword.control              | `if (x > 0)` → `if` | Control flow keywords. Fallback for import and flow keywords. |
| syntax.keyword.control.import       | `import x from 'y'` → `import` | Import/include/require statements. |
| syntax.keyword.control.flow         | `return x` → `return` | Flow control keywords (e.g., `return`, `break`, `continue`). |
| syntax.keyword.declaration          | `const age = 42;` → `const` | Declaration keywords. |
| syntax.keyword.operator             | `a + b` → `+` | Operator keywords/symbolic operators that tokenize as keywords. |
| syntax.keyword.other                | `import` → `import` | Keywords not covered by control, declaration, or operator categories. |
| syntax.storage                      | `static int x` → `static`, `int` | Storage types and modifiers. Fallback for type and modifier scopes. |
| syntax.storage.type                 | `int x` → `int` | Type keywords in declarations (e.g., `int`, `char`, `function`, `class`). |
| syntax.storage.modifier             | `public class` → `public` | Storage modifiers/qualifiers. |
| syntax.support                      | `printf` → `printf` | Library/framework-provided identifiers. Fallback for support functions, classes, types, etc. |
| syntax.support.function             | `printf` → `printf` | Library/framework functions. |
| syntax.support.class                | `String` → `String` | Library/framework classes. |
| syntax.support.type                 | `HTMLElement` → `HTMLElement` | Library/framework types. |
| syntax.support.constant             | `PI` → `PI` | Library/framework constants. |
| syntax.support.variable             | `$@special` → `$@special` | Library/framework variables. |
| syntax.support.other                | `@annotation` → `@annotation` | Other library/framework support not covered by specific categories. |
| syntax.support.function.builtin     | `len()` → `len` | Built-in/native functions. (Non-standard) |
| syntax.variable                     | `let x` → `x` | All variable references. Fallback for parameters, language variables, and function variables. |
| syntax.variable.parameter           | `function f(x)` → `x` | Function/method parameters. |
| syntax.variable.language            | `this`/`self` → `this` | Language-provided variables. |
| syntax.variable.other               | `$var` → `$var` | Other variables not covered by parameter or language. |
| syntax.variable.other.constant      | `MAX_SIZE` → `MAX_SIZE` | Constant variables. (Non-standard) |
| syntax.variable.other.object        | `obj.property` → `obj` | Object variables. (Non-standard) |
| syntax.variable.other.object        | `obj.property` → `obj` | Object variables. (Non-standard) |
| syntax.variable.other.object.property | `obj.property` → `property` | Object property variables. (Non-standard) |
| syntax.punctuation                  | `a, b;` → `,` `;` | All punctuation characters. Fallback for accessors, separators, terminators, etc. |
| syntax.punctuation.separator        | `a, b` → `,` | List/argument separators (e.g., commas, semicolons). |
| syntax.punctuation.definition       | `/* comment */` → `/* */`, `"string"` → `""` | Definition delimiters (quotes, comment markers). Fallback for string and comment delimiters. |
| syntax.punctuation.definition.string| `"hello"` → `""` | Quote delimiters for strings. |
| syntax.punctuation.definition.comment | `/* */` → `/* */` | Comment delimiters. |
| syntax.punctuation.section          | `( a )` → `(` `)` | Sectioning delimiters such as parentheses/brackets/braces. |
| syntax.markup                       | `**bold** _italic_` → `bold`, `italic` | All markup content. Fallback for bold, italic, code, links, and other markup styles. |
| syntax.markup.bold                  | `<strong>Foo Bar</strong>` → `Foo Bar` | Bold text. |
| syntax.markup.italic                | `<em>note</em>` → `note` | Italic text. |
| syntax.markup.quote                 | `<blockquote>Be yourself</blockquote>` → `Be yourself` | Quoted text. |
| syntax.markup.underline             | `<u>note</u>` → `note` | Underlined text. |
| syntax.markup.heading               | `# Title` → `Title` | Headings in markup documents. |
| syntax.markup.list                  | `- item` → `-` | All list markers. Fallback for numbered and unnumbered lists. |
| syntax.markup.list.numbered         | `1. item` → `1.` | Numbered/ordered list markers. |
| syntax.markup.list.unnumbered       | `- item` → `-` | Unnumbered/bullet list markers. |
| syntax.markup.link                  | `[text](url)` → `text` | Link text. |
| syntax.markup.raw                   | "```code```" → `code` | Raw blocks/inline code. |
| syntax.markup.inserted              | `+ const newFeature = true;` → `+ const newFeature = true;` | Inserted content in diffs or change tracking. |
| syntax.markup.changed               | `~ const version = "0.1.0";` → `~ const version = "0.1.0";` | Changed content in diffs or change tracking. |
| syntax.source                       | Embedded source code region | Source code regions (used for embedding). |
| syntax.text                         | Plain text region | Plain text regions (non-code content). |
| syntax.meta                         | `function foo() { }` → context | Meta scopes for contextual groupings (typically not styled directly). |
| syntax.meta.annotation              | `#[derive(Debug)]` → `derive` | Attribute/decorator context. (Non-standard) |
| syntax.meta.function                | `function foo() { }` → `function` | Function context (often paired with `entity.name.function`). |
| syntax.meta.class                   | `class Person {}` → `class` | Class context (often paired with `entity.name.class`). |
| syntax.meta.block                   | `{ ... }` → block | Generic block/statement grouping context. |
| syntax.meta.tag                     | `<div class="x">` → tag | Tag context in markup or templates. |
| syntax.meta.type                    | `type Foo = ...` → `type` | Type definition or declaration context. |
| syntax.meta.import                  | `import { x } from "y"` → `import` | Import/include context. |
| syntax.meta.preprocessor            | `#if DEBUG` → `#if` | Preprocessor or directive context. |
| syntax.meta.embedded                | `<style>...</style>` → embedded | Embedded language or content region. |
| syntax.meta.object                  | `obj` → `obj` | Object context. (Non-standard) |
| ui.global.background.normal         | Editor canvas → background | The general background of the user interface. |
| ui.global.background.dark           | Sidebar → background | Darker background areas, typically used for sidebars, footers, or other sections. |
| ui.global.background.light          | Active tab → background | Lighter background areas, typically used for light modes or highlighting. |
| ui.deprecated                       | `<font color="red">Hello</font>` → `<font>` | Deprecated or outdated UI elements, signaling that they are no longer recommended. |
| ui.accent                           | Focus rings / active border | Primary accent color for focus/active indications. |
| ui.border                           | Panel/tab borders | Generic border/divider color. |
| ui.cursor.normal                    | Editor caret | The text cursor color in editors. |
| ui.cursor.muted                     | Muted/disabled editor caret | The muted/disabled text cursor color in editors. |
| ui.global.foreground.normal         | Editor text → `"hello"` | General text in the user interface. |
| ui.global.foreground.dark           | Sidebar file names → `filename.md` | Text in dark-themed UI areas or sections where a lighter font is needed. |
| ui.global.foreground.light          | Active tab label → `main.js` | Light-colored text in the UI, often used in headings or highlighted sections. |
| ui.gutter.background                | Editor gutter → background | Background color for the gutter/line number area. |
| ui.gutter.foreground                | Editor gutter → line numbers | Foreground color for the gutter/line numbers. |
| ui.highlight.line.background        | Active line highlight → background | The background of the active/marked line. |
| ui.highlight.line.foreground        | Line info → text | Foreground for the line highlight area (e.g., line numbers). |
| ui.highlight.search.background      | Search highlight → background | Background of highlighted search matches. |
| ui.highlight.search.foreground      | Search highlight → text | Foreground of highlighted search matches. |
| ui.highlight.text.background        | Selected text highlight → background | Background of inline text highlights. |
| ui.highlight.text.foreground        | Selected text highlight → text | Foreground of inline text highlights. |
| ui.highlight.text.active-background | Active selection → background | Background when the selection is active/focused. |
| ui.highlight.text.active-foreground | Active selection → text | Foreground when the selection is active/focused. |
| ui.indent-guide.background          | Indent guides → background | Background color for indentation guide marks. |
| ui.indent-guide.active-background   | Active indent guide → background | Background for the active/primary indent guide. |
| ui.link                             | UI links | Link and interactive text color in UI chrome. |
| ui.whitespace.foreground            | Invisible/whitespace guides → marks | Foreground for whitespace/invisible character markers. |
| ui.selection.background             | Selected code → background | The background of selected items in the user interface (e.g., highlighted text or options). |
| ui.selection.foreground             | Selected code → foreground | The foreground of selected items in the user interface (e.g., highlighted text or options). |
| ui.selection.inactive-background    | Unfocused selection → background | Selection background when the editor is unfocused. |
| ui.status.error                     | Status/error banners | Error status/badge color. |
| ui.status.warning                   | Status/warning banners | Warning status/badge color. |
| ui.status.info                      | Status/info banners | Information status/badge color. |
| ui.status.success                   | Status/success banners | Success status/badge color. |
| ui.tooltip.background               | Tooltip/hover → background | Background of tooltips and hover popovers. |
| ui.tooltip.foreground               | Tooltip/hover → text | Foreground of tooltips and hover popovers. |

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
syntax.string.template → syntax.string → builder default (green-normal)
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

- Includes all required fields (`scheme.system`, `scheme.author`, `variant`,
  `scheme.name|scheme.slug|scheme.family` `palette`)
- Uses valid color formats (hex `#RRGGBB`)
- Follows the inheritance and structure rules defined here

All further derived or computed colors are implementation details of the
builder.

_SPEC END_

---

[Builder specification]: https://github.com/tinted-theming/home/blob/main/specs/tinted8/builder.md
[TextMate Theme structure]: https://macromates.com/manual/en/language_grammars
