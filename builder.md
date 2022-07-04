# Builder Guidelines
**Version 0.10.1**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

A base16 builder is a tool that builds application specific themeing configurations. It does this by using base16 scheme files (containing a collection of colors) and base16 template files (instructions concerning how to build the application specific files).

Builders are generally designed for template maintainers' ease of use. Template maintainers SHOULD provide built versions of their template so the end user doesn't need to be aware of the builder.

## Definitions

A _base16 scheme_ is a YAML file that represents a palette of 16 colors. For
example: the [solarized
scheme](https://github.com/base16-project/base16-schemes/blob/main/solarized-dark.yaml)

A _base16 template_ is a mustache file that acts as a blueprint; it represents
how to translate the scheme into an application's desired format. For example: the [vim
template](https://github.com/base16-project/base16-vim/blob/main/templates/default.mustache)
is used to convert a _base16 scheme_ into a vim colorscheme.

A _base16 builder_ is an application that implements the full _building_
feature specification, but MAY include additional functionality. These are
usually targeted at template maintainers or when building other base16 tooling.

_Building_ a _template_ is the process of replacing its variables (section 4.1)
with ones extracted from a _scheme_; usually outputting it to a file, as
defined by the _template_.

## Inputs

### Schemes Repository

The builder MUST provide a method of loading one or more schemes for use in building templates. The builder MAY provide a method of loading a full directory of schemes at one time. Convenient access to schemes in the [schemes repository](https://github.com/base16-project/base16-schemes) MAY also be provided.

This repo contains _scheme files_ for all base16 schemes.

- `/*.yaml`

<details>
  <summary>Scheme Files Spec</summary>

Scheme files have the following structure:

    scheme: "Scheme Name"
    author: "Scheme Author"
    description: "a short description of the scheme"
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

- Hexadecimal color values may optionally be preceded by a "#".
- Hexadecimal color values are case insensitive.

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
        extension: .file-extension
        output: output-directory-name

This example specifies that a Builder is to parse two template files: `templates/default.mustache` and `templates/additional.mustache`. `extension` defines the extension of the file that will be produced by a Builder, e.g. `base16-default-dark.file-extension`, and `output` defines the output directory that will be created within the template repository's root directory where the processed templates will be created, e.g. `output-directory-name/base16-default-dark.file-extension`.

</details>

## Template Variables

A builder MUST provide the following variables to template files:

- `scheme-name` - obtained from the `name` key of the scheme file
- `scheme-author` - obtained from the `author` key of the scheme file
- `scheme-description` - obtained from the `description` key of the scheme file (fallback value: `scheme-name`)
- `scheme-slug` - the scheme filename made lowercase with spaces, not including the `.yaml` extension
- `base00-hex` to `base0F-hex` - full hex value obtained from the scheme file. MUST NOT include a leading `#`. e.g "7cafc2".
- `base00-hex-bgr` to `base0F-hex-bgr` - built from a reversed version of all the hex values e.g "c2af7c"
- `base00-hex-r` to `base0F-hex-r` - red component of the hex color value. e.g "7c"
- `base00-hex-g` to `base0F-hex-g` - green component of the hex color value. e.g "af"
- `base00-hex-b` to `base0F-hex-b` - blue component of the hex color value. e.g "c2"
- `base00-rgb-r` to `base0F-rgb-r` - red component as a value between `0` and `255`. e.g "124"
- `base00-rgb-g` to `base0F-rgb-g` - green component as a value between `0` and `255`. e.g "175"
- `base00-rgb-b` to `base0F-rgb-b` - blue component as a value between `0` and `255` e.g "194"
- `base00-dec-r` to `base0F-dec-r` - red component as a value between `0` and `1.0`. e.g "0.4863"
- `base00-dec-g` to `base0F-dec-g` - green component as a value between `0` and `1.0`. e.g "0.6863"
- `base00-dec-b` to `base0F-dec-b` - blue component as a value between `0` and `1.0`. e.g "0.7608"

## Considerations

Mustache was chosen as the templating language due to its simplicity and widespread adoption across languages. YAML was chosen to describe scheme and configuration files for the same reasons.

The core scheme repository was based off the single scheme repository so builders supporting v0.8-v0.9 of the spec can continue to function without changes.
