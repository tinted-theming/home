# Builder Guidelines
**Version 0.11.0-dev**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

A theme builder is a tool that builds application specific themes. It does this by using scheme files (containing a palette of colors) and template files (instructions concerning how to build the application specific configuration).

Builders are generally designed for template maintainers' ease of use. Template maintainers SHOULD provide built versions of their template so the end user doesn't need to be aware of the builder.

## Glossary

A _scheme_ (or color scheme) is a generally a YAML file representing metadata about a scheme and a palette of colors. For example: the [solarized base17 scheme](https://github.com/base16-project/base17/blob/main/schemes/solarized-dark.yaml)

A _scheme system_ generally consists of a styling guide and schemes. For example [base17](https://github.com/base16-project/base17).

A _template_ is a mustache file which acts as a blueprint; it represents how to translate the scheme into an application's desired format. For example: the [base16-vim template](https://github.com/base16-project/base16-vim/blob/main/templates/default.mustache) is used to convert a _base16 scheme_ into a vim colorscheme.

A _theme builder_ is a tool which transforms color schemes and templates into application specific configuration. These are usually targeted at template maintainers or when building other theme-related tooling.

_Building a template_ is the process of replacing its variables with ones extracted from a _scheme_; usually outputting it to a file, as defined by the _template_ and _template config_.

## Inputs

Because the builder spec focuses on the provided template variables, the inputs are defined by the style systems, but must include certain information to be functional.

### Schemes

Each scheme system MUST specify a way of obtaining the following information for a given scheme, often by reading from a yaml file or some method of dynamically generating it:

* `system` - which system this scheme supports. For legacy purposes, when loading from a yaml file, if `system` is not provided, it SHOULD be assumed to be either a legacy base16 scheme or a base24 scheme depending on which colors are provided.
* `name` - the scheme's human readable name.
* `slug` - the scheme's machine readable name. The slug SHOULD use dashes rather than underscores. If it is not provided, a builder MUST infer it by [slugifying](#slugify) the scheme's name.
* `author` - the scheme's author.
* `description` - optional. A short description of the scheme.
* `palette` - all colors used by a scheme in an HTML hex format. This is case-insensitive and must be proceeded by a `#`. Some scheme systems may place additional restrictions on the palette.

<details>
  <summary>Legacy Base16 Scheme Files</summary>

**Legacy Base16 Scheme Files**

Base16 (and Base24) Scheme files have the following structure:

    scheme: "Scheme Name"
    author: "Scheme Author"
    base00: "000000"
    base01: "111111"
    base02: "222222"
    base03: "333333"
    base04: "444444"
    base05: "555555"
    base06: "666666"
    base07: "777777"
    base08: "888888"
    base09: "999999"
    base0A: "aaaaaa"
    base0B: "bbbbbb"
    base0C: "cccccc"
    base0D: "dddddd"
    base0E: "eeeeee"
    base0F: "ffffff"

When scheme is loaded in legacy mode, the following changes apply:

- `system` will be inferred as as either `base16` or `base24` depending on which bases are provided
- Hexadecimal color values MAY be preceded by a "#".
- the `palette` children MUST all be top-level, there MUST NOT be a `palette` key.
- the scheme name MUST be specified using `scheme`, not `name`.

</details>

### Template Repository

NOTE: this section is a candidate for removal in a future version. The template config spec may eventually be handled differently by different builders.

Each template repository MUST have a templates folder containing a config.yaml and any needed mustache template files.

- `/templates/*.mustache` - A template file (there may be more than one of these)
- `/templates/config.yaml` - A template configuration file

<details>
  <summary>Template Config Spec</summary>

These files have the following structure:

    default:
      supported-systems: [base16]
      filename: "output-directory-name/{{ scheme-system }}-{{ scheme-slug }}.file-extension"

    additional:
      extension: .another-extension
      output: output-directory-name

This example specifies that a Builder is to parse two template files: `templates/default.mustache` and `templates/additional.mustache`.

`filename` defines a mustache template which returns a filename relative to the template repository's root directory. All the [template variables](#template-variables) listed below are available. Builders MUST error if multiple files will be written with the same name.

`extension` and `output` are legacy options and SHOULD NOT be used by templates. If `filename` is not specified, the output filename will be `{{ output }}/{{ scheme-system }}-{{ scheme-slug }}.{{ extension }}` and will also be relative to the template repository's root directory.

As an example, the above config will output the following files for the `base16` `default-dark` color scheme:

- `output-directory-name/base16-default-dark.file-extension`, built from `default.mustache`.
- `output-directory-name/base16-default-dark.another-extension`, built from `additional.mustache`.

</details>

## Template Variables

A builder MUST provide the following variables to template files:

- `scheme-name` - obtained from the `name` key of the input
- `scheme-author` - obtained from the `author` key of the input
- `scheme-description` - obtained from the `description` key of the input
- `scheme-slug` - obtained from the `slug` key of the input (fallback value: a [slugified](#slugify) `scheme-name`)
- `scheme-system` - obtained from the `system` key of the input

Additionally, a builder MUST provide the following template variables for each defined palette token:

- `{{ token-name }}-hex` - 6-digit hex color value obtained from the scheme file. This does not include a leading `#`. e.g "7cafc2".
- `{{ token-name }}-hex-bgr` - built from a reversed version of all the hex values e.g "c2af7c"
- `{{ token-name }}-hex-r` - red component of the hex color value. e.g "7c"
- `{{ token-name }}-hex-g` - green component of the hex color value. e.g "af"
- `{{ token-name }}-hex-b` - blue component of the hex color value. e.g "c2"
- `{{ token-name }}-rgb-r` - red component as a value between `0` and `255`. e.g "124"
- `{{ token-name }}-rgb-g` - green component as a value between `0` and `255`. e.g "175"
- `{{ token-name }}-rgb-b` - blue component as a value between `0` and `255` e.g "194"
- `{{ token-name }}-dec-r` - red component as a value between `0` and `1.0`. e.g "0.4863"
- `{{ token-name }}-dec-g` - green component as a value between `0` and `1.0`. e.g "0.6863"
- `{{ token-name }}-dec-b` - blue component as a value between `0` and `1.0`. e.g "0.7608"

## Slugify

Slugify is simplest to implement in a number of passes:

* Start with your input value, replacing any Unicode characters with their ASCII aproximations (as an example é would become e). On a technical level, this can be done by normalizing the string to the Unicode NFD form (which is the decomposed version), and then dropping any combining characters.
* Replace spaces with the `-` character
* Drop all non-alphanumeric and non-dash characters

*Examples:*

* `Tomorrow Night` -> `tomorrow-night`
* `Rosé Pine` -> `rose-pine`
* `Default (Dark)` -> `default-dark`

## Considerations

Mustache was chosen as the templating language due to its simplicity and widespread adoption across languages. YAML was chosen to describe scheme and configuration files for the same reasons.
