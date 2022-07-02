# Base16 specification
**Version 0.11.0**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

## 1. Definitions

A _base16 scheme_ is an yaml file that represents a palette of 16 colors, for
use in template files. For example: the [solarized
scheme](https://github.com/base16-project/base16-schemes/blob/main/solarized-dark.yaml)

A _base16 template_ is a mustache file that acts as a blueprint; it represents
how to output the scheme into other file formats. For example: a [vim
template](https://github.com/base16-project/base16-vim/blob/main/templates/default.mustache),
to convert a _base16 scheme_ into a vim colorscheme.

A _base16 builder_ is an application that implements the full _building_
feature specification, but MAY include additional functionality. These are
usually targeted at template maintainers or when building _base16 tooling_.

Broader _base16 tooling_ refers to applications that interact with the base16
specification somehow. These include convenience software to help automate
base16 usage, as well as software that uses the architecture in other ways.

_Building_ a _template_ is the process of replacing its variables (section 4.1)
with ones extracted from a _scheme_; usually outputting it to a file, as
defined by the _template_.

## 2. Repositories and ecossystem

The main base16 ecossystem is currently composed of:
- [A single repository containing all provided _schemes_](https://github.com/base16-project/base16-schemes).
    - Most tooling would want access to all available schemes, so these were
      grouped to a single repository in version 0.8.
    - Scheme creators are free to create their own curated scheme repositories,
      but are encouraged to contribute their new schemes back to the main one.
- Repositories containing a _template set_.
    - Templates sponsored by base16 project members will be adopted and listed
      [listed](https://github.com/base16-project/base16#official-templates) on
      the [base16-project org](https://github.com/base16-project).
- Repositories containing _builder_ software.
    - Some builders will also be officially supported by and listed on the org.

## 3. Schemes

Schemes MUST be `.yaml` files containing a single map with the following keys:
- `name` - Color scheme name. MAY include any characters, including spaces and uppercase letters.
- `author` - Original and/or packager authorship information.
- `base00` to `base0F` - The 16 color themselves. MAY include leading `#`.

More information about color values are provided [at the styling
guidelines](./styling.md)

An example:
```yaml
scheme: "Solarized Dark"
author: "Ethan Schoonover (modified by aramisgithub)"
base00: "002b36"
base01: "073642"
base02: "586e75"
base03: "657b83"
base04: "839496"
base05: "93a1a1"
base06: "eee8d5"
base07: "fdf6e3"
base08: "dc322f"
base09: "cb4b16"
base0A: "b58900"
base0B: "859900"
base0C: "2aa198"
base0D: "268bd2"
base0E: "6c71c4"
base0F: "d33682"
```

## 4. Templates

A _template set_ is a single directory that MUST include the following files:
- `config.yaml` - A `.yaml` file containing a single map where each key is a
  template, which value is a map specifying which directory name it should be
  `output` to, and which `extension` the output file should have.
- One or more `.mustache` file - These are the template themselves. They should
  follow whatever structure their intended output has, with placeholders where
  colors (or scheme metadata) should be placed.

When creating template repositories, authors MUST place those files in a
directory named `templates`.

When only one template is included (or it is considered the main one), it
SHOULD be named `default.mustache`.

An example `config.yaml` defining a single template:
```yaml
default:
  extension: .ini
  output: colors
```

An example `.mustache` template:
```mustache
# Base16 foot template by h4n1
# {{scheme-name}} scheme by {{scheme-author}}
[colors]
foreground={{base06-hex}}
background={{base00-hex}}
regular0={{base01-hex}} # black
regular1={{base08-hex}} # red
regular2={{base0B-hex}} # green
regular3={{base0A-hex}} # yellow
regular4={{base0D-hex}} # blue
regular5={{base0E-hex}} # magenta
regular6={{base0C-hex}} # cyan
regular7={{base05-hex}} # white
bright0={{base02-hex}} # bright black
bright1={{base08-hex}} # bright red
bright2={{base0B-hex}} # bright green
bright3={{base0A-hex}} # bright yellow
bright4={{base0C-hex}} # bright blue
bright5={{base0E-hex}} # bright magenta
bright6={{base0F-hex}} # bright cyan
bright7={{base06-hex}} # bright white
```


## 4.1. Template variables

A compliant builder tool MUST provide the following variables to template files
it processes. That is, the following mustache variables will be replaced when
building the template:

These are obtained directly from the scheme file contents and its filename:
- `scheme-name` - obtained from the `name` key
- `scheme-author` - obtained from the `author` key
- `base00-hex` to `base0F-hex` - obtained from `base00` to `base0F` keys,
  MUST NOT include a leading `#` e.g `7cafc2`
- `scheme-slug` - the scheme filename made lowercase with spaces replaced with
  dashes

These are to be calculated based on the previous ones:
<!--
- `scheme-slug-underscored` - same as scheme-slug, but with dashes replaced with underscores
- `scheme-kind` - either "light" or "dark", calculated from the base00 color
- `scheme-is-dark` - whether `scheme-kind` is equal to `dark`
- `scheme-is-light` - whether `scheme-kind` is equal to `light`
-->
- `base00-hex-r` to `base0F-hex-r` - red component of the hex color value e.g `7c`
- `base00-hex-g` to `base0F-hex-g` - green component of the hex color value e.g `af`
- `base00-hex-b` to `base0F-hex-b` - blue component of the hex color value e.g `c2`
- `base00-hex-bgr` to `base0F-hex-bgr` - reversed version of the hex values e.g `c2af7c`
- `base00-rgb-r` to `base0F-rgb-r` - red component as a value between `0` and `255` e.g `124`
- `base00-rgb-g` to `base0F-rgb-g` - green component as a value between `0` and `255` e.g `175`
- `base00-rgb-b` to `base0F-rgb-b` - blue component as a value between `0` and `255` e.g `194`
- `base00-dec-r` to `base0F-dec-r` - red component as a value between `0` and `1.0` e.g `0.4863`
- `base00-dec-g` to `base0F-dec-g` - red component as a value between `0` and `1.0` e.g `0.6863`
- `base00-dec-b` to `base0F-dec-b` - red component as a value between `0` and `1.0` e.g `0.7608`

## 5. Building process

Builders MUST, given a _scheme_ and _template set_, replace its variables and
output the finished content in a way that makes sense with their inteded usage
or workflow. The builder MAY have the ability to work with multiple _schemes_
and/or _template sets_ at once.

The schemes and templates MAY be automatically managed by the builder or
manually by the user.

When the builder automates scheme management, they SHOULD either be fetch them
from the [scheme repository](https://github.com/base16-project/base16-schemes)
or be vendored within the builder itself.

If the builder outputs the built template(s) into files, they SHOULD follow the format:
```bash
$OUTPUT_DIR/base16-$SLUG$EXTENSION
```

Where `$SLUG` is the _scheme_ filename made lowercase with spaces replaced with
dashes (same as the `scheme-slug` variable specified in 5.1); and `$OUTPUT_DIR`
and `$EXTENSION` are, respectively, the `output` and `extension` values as
specified in the _template set_'s `config.yaml`.

## 6. Considerations
Mustache was chosen as the templating language due to its simplicity and
widespread adoption across languages. YAML was chosen to describe scheme and
configuration files for the same reasons.

Previous specification revisions included guidelines about how the builder
should fetch schemes and templates. These are now considered optional, so all
builders, including those fetching the pre-fork repositories listings, will
continue to function without changes.
