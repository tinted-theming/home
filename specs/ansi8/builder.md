# ANSI8 Builder Guidelines

**Version 0.1.0** The latest version of this spec can be obtained from
[tinted-theming/specs/ansi8/builder](https://github.com/tinted-theming/home/blob/main/specs/ansi8/builder.md)

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC
2119](https://datatracker.ietf.org/doc/html/rfc2119).*

This document describes the requirements and basic functionality of theme
builders. Builders are generally designed for template maintainers' ease of
use. Template maintainers SHOULD provide built versions of their template so
the end user doesn't need to be aware of builders.

## Inputs

Because the builder spec focuses on what template variables will be provided by
the builder, the inputs are defined by the style systems, but must provide
certain information to be functional. A common scheme format is provided here
for any palette-based scheme systems.

### Schemes

Each scheme system MUST specify a way of obtaining the following information
for a given scheme, often by reading from a `yaml` file or some method of
dynamically generating it:

* `system` - which system this scheme supports.
* `name` - the scheme's human readable name.
* `slug-stem` - optional. The scheme's machine readable name. The slug SHOULD
  use dashes rather than underscores. If it is not provided, a builder MUST infer
  it by [slugifying](#slugify) the scheme's name.
* `author` - the scheme's author.
* `variant` - optional, but recommended. Which variant of a given color scheme
  this qualifies as. Currently only "light" and "dark" are used, but this value
  could be anything.
* `palette` - all colors used by a scheme, often loaded as HTML hex colors.
  Some scheme systems may place additional restrictions on the colors in the
  palette.
* `overrides` - all color overrides used by a scheme, often loaded as HTML hex
  colors.

<details><summary>Common Scheme Format</summary>

The common scheme format is meant to be extensible so additional properties can
be added in the future.

The [schemes repository](https://github.com/tinted-theming/schemes) provides
branches for all backwards incompatible changes, so when a backwards
incompatible change is made, the same repository can continue to be used. The
main branch will always be the current stable spec. This repository has a
separate folder for each scheme system, but it is valid to walk all `yaml`
files and read them directly. All files starting with a `.` and the contents of
all directories starting with a `.` MUST be ignored.

These files have the following structure:

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

When scheme is loaded from a common scheme file, the following specifics apply:

- all color values MUST be in HTML hex format and MUST be preceded by a `#`.

</details>

### Template Config

In order to be built using a standard builder, each template repository MUST
have a templates folder containing a config.yaml and any referenced mustache
template files.

- `/templates/*.mustache` - A template file (there may be more than one of
  these)
- `/templates/config.yaml` - A template configuration file

<details>
  <summary>Template Config Spec</summary>

These files have the following structure:

```yaml
default:
  supported-systems: [ansi8]
  filename: "output-directory-name/{{ scheme-system }}-{{ scheme-slug }}.file-extension"

additional:
  extension: .another-extension
  output: output-directory-name
```

This example specifies that a Builder is to parse two template files:
`templates/default.mustache` and `templates/additional.mustache`.

`supported-systems` defines a list containing all scheme systems this template
should be rendered for. This defaults to an array containing only `base16`.

`filename` defines a mustache template which returns a filename relative to the
template repository's root directory. All the [template
variables](#template-variables) listed below are available. Builders MUST error
if multiple files will be written with the same name.

`extension` and `output` are legacy options and SHOULD NOT be used by
templates. If `filename` is not specified, the output filename will be `{{
output }}/{{ scheme-system }}-{{ scheme-slug }}.{{ extension }}`, relative to
the template repository's root directory.

As an example, the above config will output the following files for the
`base16` `default-dark` color scheme:

- `output-directory-name/base16-default-dark.file-extension`, built from
  `default.mustache`.
- `output-directory-name/base16-default-dark.another-extension`, built from
  `additional.mustache`.

</details>

## Slugify

Slugify is simplest to implement in a number of passes:

- Start with your input value, replacing any Unicode characters with their
  ASCII approximations (as an example `é` would become `e`). On a technical
  level, this can be done by normalizing the string to the Unicode NFD form
  (which is the decomposed version), and then dropping any combining characters.
- Lowercase all characters. (convert characters `A` to `Z`, to `a` to `z`.)
- Replace spaces with the `-` character
- Drop all characters that are neither alphanumeric nor dashes

**Examples:**

- `Tomorrow Night` -> `tomorrow-night`
- `Rosé Pine` -> `rose-pine`
- `Default (Dark)` -> `default-dark`

## Considerations

Mustache was chosen as the templating language due to its simplicity and
widespread adoption across languages. YAML was chosen to describe scheme and
configuration files for the similar reasons.

## Template Variables

### Meta variables

| Variable Name                   | Description |
| ------------------------------- | ----------- |
| `scheme-name`                   | Obtained from the `name` key of the scheme input |
| `scheme-author`                 | Obtained from the `author` key of the scheme input |
| `scheme-description`            | obtained from the `description` key of the scheme input |
| `scheme-slug`                   | obtained from the `slug` key of the scheme input (fallback value: a [slugified](#slugify) `scheme-name`) |
| `scheme-slug-underscored`       | the `scheme-slug` template variable where dashes have been replaced with underscores |
| `scheme-system`                 | obtained from the `system` key of the scheme input|
| `scheme-variant`                | obtained from the `variant` key of the scheme input |
| `scheme-is-{{variant}}-variant` | dynamic value built from the `variant` key of the scheme file. e.g. `variant: "light"` provides `scheme-is-light-variant` with a value of `true`.|

### Palette

Some general rules:

- Each scheme palette token is directly mapped to `{{token-name}}-default` - a
  `default` color-varaint.
- Each `default` color vaiant has a matching `bright` and `dim` color-variant.
- `gray` is not a `token-name`, but `gray-default` is generated by finding the
  mid-point of the `black` and `white` palette token values.
- `brown` is not a `token-name`, but `brown-default` is generated by darkening
  the `red` token value and adjusting the hue by `TODO`.

In addition to the "Meta varaibles", a builder MUST provide the following
template variables for each defined palette token and color-variant:

| Variable Name                              | Description |
| ------------------------------------------ | ----------- |
| `{{token-name}}-{{token-variant}}-hex`     | 6-digit hex color value. This does not include a leading `#`. e.g "7cafc2".|
| `{{token-name}}-{{token-variant}}-hex-bgr` | built from a reversed version of all the hex values e.g "c2af7c" |
| `{{token-name}}-{{token-variant}}-hex-r`   | red component of the hex color value. e.g "7c" |
| `{{token-name}}-{{token-variant}}-hex-g`   | green component of the hex color value. e.g "af" |
| `{{token-name}}-{{token-variant}}-hex-b`   | blue component of the hex color value. e.g "c2" |
| `{{token-name}}-{{token-variant}}-rgb-r`   | red component as a value between `0` and `255`. e.g "124" |
| `{{token-name}}-{{token-variant}}-rgb-g`   | green component as a value between `0` and `255`. e.g "175" |
| `{{token-name}}-{{token-variant}}-rgb-b`   | blue component as a value between `0` and `255` e.g "194" |
| `{{token-name}}-{{token-variant}}-rgb16-r` | 16 bit red component as a value between `0` and `65_535`. e.g "15000" |
| `{{token-name}}-{{token-variant}}-rgb16-g` | 16 bit green component as a value between `0` and `65_535`. e.g "30000" |
| `{{token-name}}-{{token-variant}}-rgb16-b` | 16 bit blue component as a value between `0` and `65_535` e.g "60000" |
| `{{token-name}}-{{token-variant}}-dec-r`   | red component as a value between `0` and `1.0`. e.g "0.4863" |
| `{{token-name}}-{{token-variant}}-dec-g`   | green component as a value between `0` and `1.0`. e.g "0.6863" |
| `{{token-name}}-{{token-variant}}-dec-b`   | blue component as a value between `0` and `1.0`. e.g "0.7608" |

Additionally, a builder MUST generate `gray-{{token-variant}}` and
`brown-{{token-variant}}` which MUST also have the above variables.

**Note**: There are colors that aren't currently used for anything yet, this is
because the spec is new and we're still figuring out what the styling should be
exactly.

### Overrides

The palette variable name color values will be known as "template-variable-color-type".

In addition to the template variables already mentioned, a builder MUST provide
the following template variables:

| Variable Name                                                            |
| ------------------------------------------------------------------------ |
| `override-comment-{{template-variable-color-type}}`                      |
| `override-string-{{template-variable-color-type}}`                       |
| `override-string-quoted-{{template-variable-color-type}}`                |
| `override-string-regexp-{{template-variable-color-type}}`                |
| `override-constant-{{template-variable-color-type}}`                     |
| `override-constant-numeric-{{template-variable-color-type}}`             |
| `override-constant-numeric-integer-{{template-variable-color-type}}`     |
| `override-constant-numeric-float-{{template-variable-color-type}}`       |
| `override-constant-numeric-exponential-{{template-variable-color-type}}` |
| `override-constant-language-boolean-{{template-variable-color-type}}`    |
| `override-constant-character-{{template-variable-color-type}}`           |
| `override-constant-character-entity-{{template-variable-color-type}}`    |
| `override-constant-character-escape-{{template-variable-color-type}}`    |
| `override-entity-name-{{template-variable-color-type}}`                  |
| `override-entity-name-class-{{template-variable-color-type}}`            |
| `override-entity-name-function-{{template-variable-color-type}}`         |
| `override-entity-name-tag-{{template-variable-color-type}}`              |
| `override-entity-name-variable-{{template-variable-color-type}}`         |
| `override-entity-other-attributeName-{{template-variable-color-type}}`   |
| `override-keyword-{{template-variable-color-type}}`                      |
| `override-keyword-control-{{template-variable-color-type}}`              |
| `override-keyword-declaration-{{template-variable-color-type}}`          |
| `override-markup-{{template-variable-color-type}}`                       |
| `override-markup-bold-{{template-variable-color-type}}`                  |
| `override-markup-code-{{template-variable-color-type}}`                  |
| `override-markup-italic-{{template-variable-color-type}}`                |
| `override-markup-quote-{{template-variable-color-type}}`                 |
| `override-diff-added-{{template-variable-color-type}}`                   |
| `override-diff-changed-{{template-variable-color-type}}`                 |
| `override-diff-deleted-{{template-variable-color-type}}`                 |
| `override-ui-background-{{template-variable-color-type}}`                |
| `override-ui-backgroundDark-{{template-variable-color-type}}`            |
| `override-ui-backgroundLight-{{template-variable-color-type}}`           |
| `override-ui-deprecated-{{template-variable-color-type}}`                |
| `override-ui-foreground-{{template-variable-color-type}}`                |
| `override-ui-foregroundDark-{{template-variable-color-type}}`            |
| `override-ui-foregroundLight-{{template-variable-color-type}}`           |
| `override-ui-lineBackground-{{template-variable-color-type}}`            |
| `override-ui-searchText-{{template-variable-color-type}}`                |
| `override-ui-selectionBackground-{{template-variable-color-type}}`       |

The above overrides template variable values are overwritten by the optional
scheme defined override token. The following overwrites
`override-comment-{{template-variable-color-type}}` to derive the values from
the hex value `#555555` instead of from `gray_dim`.

```yaml
...
override:
  comment: "#555555"
...
```

_SPEC END_

---
