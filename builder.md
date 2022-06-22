# Builder Guidelines
**Version 0.11.0**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

## Introduction

A base16 builder is, essentially, an application that can build base16
templates with base16 [schemes](./styling.md).

A template is a "blueprint" that specifies a file representing how to use the
16 base16 colors with that specific software/format. For example: a
[colorscheme template for vim](https://github.com/base16-project/base16-vim).

A scheme is a color palette that consists of 16 colors (hence the name). For
example: [the solarized scheme](https://github.com/base16-project/base16-schemes/blob/main/solarized-dark.yaml)

Builders are designed for lower-level ("plumbing") usage, specifically for
scripting and as component to build more complex base16 applications, designed
for end users ("porcelain").

Template maintainers SHOULD provide built versions (with all existing scheme)
so the end user doesn't need to be aware of the builder.

## Interface

All base16 builders MUST provide a single feature: building a template using 1 or more schemes.

### CLI

It is REQUIRED that that this functionality is exposed as binary CLI executable
with the exact interface described below.

To be fully compliant, a builder CLI interface MUST NOT include any other
feature, option, argument, or deviance from the expected interface and
behaviour of the program.

<!-- TODO: For convenience, we make a manpage and set of tests available. All
compliant builders MUST fully conform to these two. -->

The CLI interface MUST work without relying on any network connection.

```bash
base16 TEMPLATES-DIRECTORY SCHEME-FILE ...
```

`TEMPLATES-DIRETORY` being a directory containing a `config.yaml`, as well as at
least one `.mustache` template. These are usually named `templates` on all
base16 template repositories.

`SCHEME-FILE` being one or more `.yaml` scheme file. The main source for these
is the [base16-schemes](https://github.com/base16-project/base16-schemes)
repository.

The program MAY offer a single `--debug | -d` option for increasing log
verbosity. These are considered implementation detail and each author SHOULD
implement them as they see fit.

### Library

The compliant base16 builder software MAY also expose a software library other
developers may use to assist developing more complex base16-compatible
software.

This exposed library, or any internal code, has no required structure or usage.

The author MAY choose how they will expose these functionalities to the caller,
according to their preferences and SHOULD follow best practices on their
respective programming languages.

It is RECOMMENDED that builders follow semantic versioning for their library
interface.

The author MAY implement additional features that are exposed through the
library, as long as it does not affect the CLI functionality compliance.

## Output and behaviour

**Note**: As the CLI is not intended for usual human usage, all outputted text
messages are considered implementation detail, so the author MAY output
whatever they prefer (or no message at all). If needed, scripts using the
builder SHOULD check for return codes (specified below) instead of messages.

For all templates defined in the template config file (`config.yaml`, inside
the specified template directory), the builder MUST iterate through all the
defined schemes and output matching files.

The built filename should look like [output-dir]/base16-[slug][extension],
where the slug is taken from the scheme filename made lowercase with spaces
replaced with dashes and both the extension and output-dir are taken from
`config.yaml`.

The builder MUST check for the (unusual) case where schemes share the same
slug, in this case the program MUST exit with code `1` and MAY output an error
message.

If the build fails for whatever other reasons, the program MUST exit with code
`2` and MAY output an error message.

## Template Variables
A builder MUST provide the following variables to the template files it
processes:

- `scheme-name` - obtained from the scheme file
- `scheme-author` - obtained from the scheme file
- `scheme-slug` - obtained from the scheme filename, as described above

- `base00-hex` to `base0F-hex` - obtained from the scheme file e.g "7cafc2"
- `base00-hex-r` to `base0F-hex-r` - built from the hex value in the scheme file e.g "7c"
- `base00-hex-g` to `base0F-hex-g` - built from the hex value in the scheme file e.g "af"
- `base00-hex-b` to `base0F-hex-b` - built from the hex value in the scheme file e.g "c2"
- `base00-hex-bgr` to `base0F-hex-bgr` - built from a reversed version of all the hex values e.g "c2af7c"

- `base00-rgb-r` to `base0F-rgb-r` - converted from the hex value in the scheme file e.g "124"
- `base00-rgb-g` to `base0F-rgb-g` - converted from the hex value in the scheme file e.g "175"
- `base00-rgb-b` to `base0F-rgb-b` - converted from the hex value in the scheme file e.g "194"
- `base00-dec-r` to `base0F-dec-r` - converted from the rgb value in the scheme file e.g "0.87..."
- `base00-dec-g` to `base0F-dec-g` - converted from the rgb value in the scheme file e.g "0.50..."
- `base00-dec-b` to `base0F-dec-b` - converted from the rgb value in the scheme file e.g "0.21..."

## Considerations
Mustache was chosen as the templating language due to its simplicity and
widespread adoption across languages. YAML was chosen to describe scheme and
configuration files for the same reasons.

The core scheme repository was based off the single scheme repository so
builders supporting v0.8-v0.9 of the spec can continue to function without
changes.

The revised builder functionality specification introduced in v0.11 did not
introduce any changes to schemes or templates, so no changes to these are
needed Older builders will continue to work, but authors are encouraged to
implement the new, simpler and more consistent, specification.
