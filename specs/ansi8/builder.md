# Tinted8 Builder Guidelines

**Version 0.1.0** The latest version of this spec can be obtained from
[tinted-theming/specs/tinted8/builder](https://github.com/tinted-theming/home/blob/main/specs/tinted8/builder.md)

## Introduction

Builders convert a Tinted8 scheme into color data for templates to generate
themes.

## Inputs

### Scheme Inputs

Builders read scheme files that conform to the Styling specification. At
minimum they must provide:

- `system`, `scheme-author`, `variant`, `name|slug|family`, `palette`
- Optional `overrides`

All color values must be HTML-style hex (``#RRGGBB`).

### Template Input

```
/templates/config.yaml
/templates/*.mustache
```

`config.yaml` describes which systems the template supports and how output
filenames are constructed. Builders read these values to generate consistent
output paths.

## Name and Slug Handling

If a scheme lacks a `slug`, builders derive one by slugifying the `name`:

- Normalize Unicode to ASCII
- Lowercase all letters
- Replace spaces with `-`
- Remove non-alphanumeric, non-dash characters

Examples: 

- `Tomorrow Night` → `tomorrow-night`
- `Rosé Pine` → `rose-pine`

If name is missing, builders may infer it from family + flavor.

## Palette Expansion

### Variants

For every `palette.<color>`, builders generate:

- `default` - The color as provided (e.g. `red-default`)
- `bright` - A lighter variant (e.g. `cyan-bright`)
- `dim` - A darker variant (e.g `green-dim`)

### Derived Colors

Supplimental colors are generated if they aren't provided in the scheme itself:

- `gray` - The midpoint between `palette.black` and `palette.white`
- `orange` - Hue-shifted variant of `palette.yellow`
- `brown` - A deeper desaturated variant of `palette.red`

### Naming

Each produced value is exposed as:

```
{{token-name}}-{{variant}}
```

e.g. `blue-bright`, `green-dim`.

Builders may also expose sub-components:

```
{{token-name}}-{{variant}}-hex   → "7cafc2"
{{token-name}}-{{variant}}-rgb-r → "124"
{{token-name}}-{{variant}}-dec-b → "0.76"
```

The full list of component variables mirrors standard RGB breakdowns.

## Template Variables

### Meta Variables

| Variable                  | Type    | Source                                                  |
| ------------------------- |-------- | ------------------------------------------------------- |
| `scheme-name`             | String  | `name`                                                  |
| `scheme-author`           | String  | `author`                                                |
| `scheme-description`      | String  | `description`                                           |
| `scheme-slug`             | String  | `slug` or slugified `name` seperated by hiphens `-`     |
| `scheme-slug-underscored` | String  | `slug` or slugified `name` seperated by underscores `_` |
| `scheme-system`           | String  | `system`                                                |
| `scheme-variant`          | String  | `variant`                                               |
| `scheme-is-dark-variant`  | Boolean | Based on `scheme-variant` value                         | 

### Color Variables

The builder provides various color variables for every `palette` token variant
(`default`, `bright`, `dim`) and every override key.

The variable suffixes are as follows:

- `{{ token-name }}-hex` - 6-digit hex color value (e.g "7cafc2")
- `{{ token-name }}-hex-<r|g|b>` - Provides a R, G or B hex color value (e.g "7c")
- `{{ token-name }}-hex-bgr` - A reversed version of all the hex values (e.g "c2af7c")
- `{{ token-name }}-rgb-<r|g|b>` - Provides a R, G or B color value between `0` and `255` (e.g. "124")
- `{{ token-name }}-dec-<r|g|b>` - Provides a R, G or B decimal value between `0` and `1` (e.g. "0.4863")
- `{{ token-name }}-rgb16-<r|g|b>` - Provides a R, G or B 16 bit value between `0` and `65_535` (e.g. "15000")

For example:

```
override-comment-hex
override-string-dec-r
override-ui-background-rgb16-b
```

Values omit the leading `#` for hex strings.

### Override Variables

For every recognized override key from the Styling spec, builders provide
equivalent template variables, for example:

```
override-comment-hex
override-string-dec-r
override-ui-background-rgb16-b
```

Each corresponds either to:

1. The explicit override in the scheme
1. Its inherited parent
1. The builder's default color token

## Override Resolution

Resolution order:

- Explicit scheme override – exact key value (e.g. `override.diff.added`)
- Inherited override – parent group value (e.g. `override.diff`)
- Builder default – mapped palette token (e.g. `green_bright`)

Builders must ensure all override variables resolve to a valid color.

### Builder Default Colors

| Override Property                     | Default Color   |
| ------------------------------------- | --------------- |
| override.comment                      | gray_dim        |
| override.string                       | green_default   |
| override.constant                     | yellow_default  |
| override.constant.character           | yellow_default  |
| override.entity.name                  | yellow_default  |
| override.entity.other.attributeName   | yellow_bright   |
| override.keyword                      | magenta_default |
| override.markup                       | cyan_default    |
| override.diff.added                   | green_bright    |
| override.diff.changed                 | magenta_bright  |
| override.diff.deleted                 | red_bright      |
| override.ui.background                | black_default   |
| override.ui.backgroundDark            | black_dim       |
| override.ui.backgroundLight           | black_bright    |
| override.ui.deprecated                | brown_default   |
| override.ui.foreground                | white_default   |
| override.ui.foregroundDark            | gray_bright     |
| override.ui.foregroundLight           | white_bright    |
| override.ui.lineBackground            | gray_dim        |
| override.ui.searchText                | yellow_default  |
| override.ui.selectionBackground       | black_bright    |

## Output and Template Config

Builders apply template configuration as follows:

- Respect `supported-systems`
- Generate output filenames according to the `filename` template (with
  available variables)
- Avoid name collisions
- Write rendered templates relative to the repository root

Example `config.yaml`:

```yaml
default:
  filename: "output/{{ scheme-system }}-{{ scheme-slug }}.ext"
  supported-systems: [tinted8]
```

## Compliance

A builder is considered **Tinted8-compliant** if it:

- Correctly reads Tinted8 scheme files
- Expands all palette and override variables
- Provides consistent variable naming for templates
- Generates derived colors as described above

## Design Considerations

Tinted8 builders are encouraged to:

- Maintain perceptual contrast between bright/dim variants
- Preserve hue relationships when computing derived colors
- Cache computed variables for performance
- Provide clear error messages for missing or invalid fields

## Considerations

Mustache was chosen as the templating language due to its simplicity and
widespread adoption across languages. YAML was chosen to describe scheme and
configuration files for the similar reasons.

The other Tinted Theming scheme systems also use Mustache and YAML, making it a
consistent choice.

## References

- Tinted8 Styling Specification v0.1.0-draft
- Mustache Template Language Specification

_SPEC END_

---

[semver]: https://semver.org/
