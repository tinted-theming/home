# Builder Guidelines
**Version 0.11.0-dev**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

A theme builder is a tool that builds application specific themeing configurations. It does this by using scheme files (containing a collection of colors) and template files (instructions concerning how to build the application specific files).

Builders are generally designed for template maintainers' ease of use. Template maintainers SHOULD provide built versions of their template so the end user doesn't need to be aware of the builder.

## Definitions

A _scheme_ is a YAML file which represents a palette of colors. For
example: the [solarized
scheme](https://github.com/base16-project/base16-schemes/blob/main/solarized-dark.yaml)

A _template_ is a mustache file which acts as a blueprint; it represents
how to translate the scheme into an application's desired format. For example: the [base16-vim
template](https://github.com/base16-project/base16-vim/blob/main/templates/default.mustache)
is used to convert a _base16 scheme_ into a vim colorscheme.

A _theme builder_ is an application that implements the full _building_
feature specification, but MAY include additional functionality. These are
usually targeted at template maintainers or when building other theme-related tooling.

_Building_ a _template_ is the process of replacing its variables (section 4.1)
with ones extracted from a _scheme_; usually outputting it to a file, as
defined by the _template_ and _template config_.

## Inputs

### Schemes Repository

The builder MUST provide a method of loading one or more schemes for use in building templates. The builder MAY provide a method of loading multiple schemes at one time. Convenient access to schemes in the [schemes repository](https://github.com/base16-project/base16-schemes) MAY also be provided.

This repo contains _scheme files_ for all official schemes. We store scheme styles in different directories, but this is not a guarantee.

- `/base16/*.yaml`
- `/base24/*.yaml`

This could alternatively be expressed as this:

- `**/*.yaml`

<details>
  <summary>Scheme Files Spec</summary>

Scheme files have the following structure:

    scheme: "Scheme Name"
    author: "Scheme Author"
    description: "a short description of the scheme"
    style: base16
    colors:
      base00: "#000000"
      base01: "#111111"
      base02: "#222222"
      base03: "#333333"
      base04: "#444444"
      base05: "#555555"
      base06: "#666666"
      base07: "#777777"
      base08: "#888888"
      base09: "#999999"
      base0A: "#aaaaaa"
      base0B: "#bbbbbb"
      base0C: "#cccccc"
      base0D: "#dddddd"
      base0E: "#eeeeee"
      base0F: "#ffffff"

- Hexadecimal color values MUST be preceded by a "#".
- Hexadecimal color values are case insensitive.
- If style is not provided it will default to "base16".
- In previous versions of the spec, all the base16 colors were defined as top-level keys, so builders SHOULD support old style base16 schemes as well.

</details>

### Template Repository

Each template repository MUST have a templates folder containing a config.yaml and any needed mustache template files.

- `/templates/*.mustache` - A template file (there may be more than one of these)
- `/templates/config.yaml` - A template configuration file

<details>
  <summary>Template Config Spec</summary>

These files have the following structure:

    default:
      extension: .file-extension
      output: output-directory-name

    additional:
      styles: [base16]
      filename: "output-directory-name/{{ scheme-style }}-{{ scheme-slug }}.file-extension"

This example specifies that a Builder is to parse two template files: `templates/default.mustache` and `templates/additional.mustache`. `extension` defines the extension of the file that will be produced by a Builder, e.g. `base16-default-dark.file-extension`, and `output` defines the output directory that will be created within the template repository's root directory where the processed templates will be created, e.g. `output-directory-name/base16-default-dark.file-extension`. The `styles` key defaults to an array containing only `base16` and limits which schemes will be built for these templates.

If more control over the output filename is needed, `filename` can be used. It defines a mustache template which returns a filename relative to the template repository's root directory. All the template variables listed below are available.

</details>

## Template Variables

A builder MUST provide the following variables to template files:

- `scheme-name` - obtained from the `scheme` key of the scheme file
- `scheme-author` - obtained from the `author` key of the scheme file
- `scheme-description` - obtained from the `description` key of the scheme file (fallback value: `scheme-name`)
- `scheme-slug` - the scheme filename made lowercase, not including the `.yaml` extension
- `scheme-style` - obtained from the `style` key of the scheme file (fallback value: "base16")

Additionally, a builder MUST provide the following variables for each defined color:

- `{{ color-name }}-hex` - 6-digit hex color value obtained from the scheme file. MUST NOT include a leading `#`. e.g "7cafc2".
- `{{ color-name }}-hex-bgr` - built from a reversed version of all the hex values e.g "c2af7c"
- `{{ color-name }}-hex-r` - red component of the hex color value. e.g "7c"
- `{{ color-name }}-hex-g` - green component of the hex color value. e.g "af"
- `{{ color-name }}-hex-b` - blue component of the hex color value. e.g "c2"
- `{{ color-name }}-rgb-r` - red component as a value between `0` and `255`. e.g "124"
- `{{ color-name }}-rgb-g` - green component as a value between `0` and `255`. e.g "175"
- `{{ color-name }}-rgb-b` - blue component as a value between `0` and `255` e.g "194"
- `{{ color-name }}-dec-r` - red component as a value between `0` and `1.0`. e.g "0.4863"
- `{{ color-name }}-dec-g` - green component as a value between `0` and `1.0`. e.g "0.6863"
- `{{ color-name }}-dec-b` - blue component as a value between `0` and `1.0`. e.g "0.7608"

## Considerations

Mustache was chosen as the templating language due to its simplicity and widespread adoption across languages. YAML was chosen to describe scheme and configuration files for the same reasons.
