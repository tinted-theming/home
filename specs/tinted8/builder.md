# Tinted8 Builder Guidelines

**Version 0.1.0** The latest version of this spec can be obtained from
[tinted-theming/specs/tinted8/builder]

## Introduction

Builders convert a Tinted8 scheme into color data for templates to generate
themes.

## Inputs

### Scheme Inputs

Builders read scheme files that conform to the Styling specification. At
minimum they must provide:

- Required: `system`, `scheme-author`, `variant`, `palette`
- Partially required: At least one of `name`, `slug` or `family`
- Optional: `syntax`, `ui`, `style`, `theme-author`, `description`

All color values must be HTML-style hex (`#RRGGBB`).

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

- `Catppuccin Mocha` → `catppuccin-mocha`
- `Rosé Pine` → `rose-pine`
- `Default (Dark)` → `default-dark`

## Palette Expansion

### Variants

For every `palette.{{token_name}}`, if the color is missing, the builder generates:

- `default` - The color as provided (e.g. `red-default`)
- `bright` - A lighter variant (e.g. `cyan-bright`)
- `dim` - A darker variant (e.g `green-dim`)

### Derived Colors (when missing)

Supplemental colors are generated if they aren't provided in the scheme itself.
If a color is present in the scheme palette it must be used as-is; otherwise it
is derived using the formulas below:

- `gray` - The midpoint between `palette.black` and `palette.white`.
- `orange` - A hue-shifted variant of `palette.yellow`.
- `brown` - A darker, desaturated variant derived from `palette.yellow`.

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

## Color Formulas

This section defines the normative color conversion rules builders must apply
when deriving supplemental colors and generating `bright`/`dim` variants. Unless
stated otherwise, conversions operate in HSL with channel ranges `S, L ∈ [0,1]`
and hue in degrees `h ∈ [0, 360)`.

- Clamp: `clamp(x, lo, hi) = min(max(x, lo), hi)`; builders must clamp `S` and
  `L` after each operation to remain in-range.
- Hue wrap: add/subtract in degrees and wrap with `(h + 360) % 360`.

### Derived Colors (when missing)

- orange from yellow
  - Input: `h, s, l = HSL(palette.yellow)`
  - Operation: `h' = (h - 10) mod 360`, `s' = s`, `l' = l`
  - Output: `HSL(h', s', l')` converted back to RGB/hex

- brown from yellow
  - Input: `h, s, l = HSL(palette.yellow)`
  - Operation: `h' = h`, `s' = clamp(s - 0.30, 0, 1)`, `l' = clamp(l - 0.40, 0, 1)`
  - Output: `HSL(h', s', l')` converted back to RGB/hex

- gray from black and white
  - Input: `HSL(black) = (h_b, s_b, l_b)`, `HSL(white) = (h_w, s_w, l_w)`
  - Operation:
    - Hue midpoint (wrap-aware): `d = ((h_b - h_w + 540) % 360) - 180`, `h' = (h_w + 0.5*d + 360) % 360`
    - Saturation: `s' = 0`
    - Lightness: `l' = 0.5 * (l_b + l_w)`
  - Output: `HSL(h', s', l')` converted back to RGB/hex

If the scheme provides any of `orange`, `brown` or `gray`, builders must not
override them and should skip derivation for that color.

### Variant Generation (bright/dim)

Builders must derive missing `bright` and `dim` from the `default` variant of
each palette color using the following HSL adjustments, leaving the hue
unchanged.

- Constants: `ΔL = 0.12`

- dim
  - Given `HSL(h, s, l)`:
  - Lightness: `l' = clamp(l - min(ΔL, l), 0, 1)`
  - Saturation boost factor `k_dim(l)`:
    - if `l < 0.4` → `k = 1.04`
    - else if `l < 0.7` → `k = 1.07`
    - else → `k = 1.10`
  - Saturation: `s' = clamp(s * k, 0, 1)`

- bright
  - Given `HSL(h, s, l)`:
  - Lightness: `l' = clamp(l + min(ΔL, 1 - l), 0, 1)`
  - Saturation factor `k_bright(l)`:
    - if `l < 0.5` → `k = 1.08`
    - else if `l < 0.8` → `k = 1.00`
    - else → `k = 0.90`
  - Saturation: `s' = clamp(s * k, 0, 1)`

These rules ensure consistent perceived contrast between `default`, `dim`, and
`bright` variants while avoiding out-of-gamut values.

## Template Variables

### Meta Variables

| Variable                  | Type    | Source                                                    |
| ------------------------- |-------- | --------------------------------------------------------- |
| `scheme-name`             | String  | `name`                                                    |
| `scheme-author`           | String  | `author`                                                  |
| `scheme-description`      | String  | `description`                                             |
| `scheme-slug`             | String  | `slug` or slugified `name` seperated by hiphens (`-`)     |
| `scheme-slug-underscored` | String  | `slug` or slugified `name` seperated by underscores (`_`) |
| `scheme-system`           | String  | `system`                                                  |
| `scheme-variant`          | String  | `variant`                                                 |
| `scheme-is-dark-variant`  | Boolean | Based on `scheme-variant` value                           | 

### Color Variables

`syntax` and `ui` properties will be referred to as "Theming Properties".

The builder provides various color variables for every `palette` token variant
(`default`, `bright`, `dim`) and every Theming Property.

The variable suffixes are as follows:

- `{{token-name}}-hex` - 6-digit hex color value (e.g "7cafc2")
- `{{token-name}}-hex-<r|g|b>` - Provides a R, G or B hex color value (e.g "7c")
- `{{token-name}}-hex-bgr` - A reversed version of all the hex values (e.g "c2af7c")
- `{{token-name}}-rgb-<r|g|b>` - Provides a R, G or B color value between `0` and `255` (e.g. "124")
- `{{token-name}}-dec-<r|g|b>` - Provides a R, G or B decimal value between `0` and `1` (e.g. "0.4863")
- `{{token-name}}-rgb16-<r|g|b>` - Provides a R, G or B 16 bit value between `0` and `65_535` (e.g. "15000")

Values omit the leading `#` for hex strings.

### Theming Properties

For every recognized `syntax` and `ui` key from the Styling spec, builders
provide equivalent template variables, for example:

```
syntax-comment-hex
syntax-string-dec-r
ui-background-rgb16-b
```

Each corresponds either to:

1. The explicit values set in the scheme
1. Its inherited parent
1. The builder's default color token

## Theme Resolution

Resolution order:

1. Explicit scheme Theming Property - exact key value (e.g. `syntax.diff.added`)
1. Inherited Theming Property - parent group value (e.g. `syntax.diff`)
1. Builder default - mapped palette token (e.g. `green_bright`)

Builders must ensure all Theming Properties resolve to a valid color.

### Builder Default Colors

| Theming Property                   | Default Color   |
| ---------------------------------- | --------------- |
| syntax.comment                     | gray_dim        |
| syntax.string                      | green_default   |
| syntax.constant                    | yellow_default  |
| syntax.constant.character          | yellow_default  |
| syntax.entity.name                 | yellow_default  |
| syntax.entity.other.attribute-name | yellow_bright   |
| syntax.keyword                     | magenta_default |
| syntax.markup                      | cyan_default    |
| syntax.diff.added                  | green_bright    |
| syntax.diff.changed                | magenta_bright  |
| syntax.diff.deleted                | red_bright      |
| ui.background                      | black_default   |
| ui.background-dark                 | black_dim       |
| ui.background-light                | black_bright    |
| ui.deprecated                      | brown_default   |
| ui.foreground                      | white_default   |
| ui.foreground-dark                 | gray_bright     |
| ui.foreground-light                | white_bright    |
| ui.line-background                 | gray_dim        |
| ui.search-text                     | yellow_default  |
| ui.selection-background            | black_bright    |

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

## Version and Specification Support

Tinted8 builders must declare and validate the specification versions they support
to ensure compatibility across the Styling and Builder specifications.

### Support Declaration

Every builder **must expose** a `supports` object, either in its configuration or
metadata output, with the following fields in the `templates/config.yaml`:

```yaml
default:
  filename: "output/{{ scheme-system }}-{{ scheme-slug }}.ext"
  supported-systems: [tinted8]
  supports:
    tinted8-styling: ">=0.1.0"
    tinted8-builder: ">=0.1.0"
```

This defines which versions of the Tinted8 Styling and Builder specifications
are implemented and guaranteed compatible. All `supports` object property
values must follow semantic versioning rules ([semver]).

### Enforcement

When loading a scheme file, the builder must check that:

1. The scheme's declared system matches "tinted8".
1. The scheme's spec version (if provided) satisfies the builder's
   `supports.tinted8-styling` range.
1. The builder's own implementation version satisfies its declared
   `supports.tinted8-builder` range.

If any of these checks fail, the builder must emit an error and refuse to
process the scheme until the version mismatch is resolved.

### Example Validation Flow

```
flowchart TD
  A[Scheme.yaml] → B{system == "tinted8"?}
  B → |No| E[Error: E001 Invalid system]
  B → |Yes| C{tinted8-styling version within supported range?}
  C → |No| F[Error: E002 Unsupported Tinted8 Styling Spec]
  C → |Yes| D{tinted8-builder self-version within supported range?}
  D → |No| G[Error: E003 Tinted8 Builder Spec Incompatible]
  D → |Yes| H[Proceed with build]
```

### Example CLI Output

```
$ tinted8-builder build ./
✔ system: tinted8
✔ tinted8-styling: v0.1.0 (supported range >=0.1.0)
✔ tinted8-builder: v0.1.0 (self-compatible)
→ Building theme...
```

If validation fails:

```
✖ Error E002: Scheme requires Styling v0.2.0 but tinted8-builder supports only >=0.1.0
```

### Rationale

This ensures:

- Builders only build versions they are designed for, which will reduce builder generation bugs
- Builders will have backward compatibility built into them for both the builder and styling specifications
- Authors can easily identify compatibility issues
- Downstream tools (editors, integrations) can introspect supported specs programmatically

| Code   | Description                                                        |
| ------ | ------------------------------------------------------------------ |
| `E001` | Invalid or missing `supported-systems` field.                      |
| `E002` | Scheme requires unsupported Tinted8 Styling spec version.          |
| `E003` | Builder version not compatible with declared Tinted8 Builder spec. |

## Compliance

A builder is considered **Tinted8-compliant** if it:

- Correctly reads Tinted8 scheme files
- Expands all palette and Theming Properties
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

[tinted-theming/specs/tinted8/builder]: https://github.com/tinted-theming/home/blob/main/specs/tinted8/builder.md
[semver]: https://semver.org/
