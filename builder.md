# Base16 builder specification
**Version 0.11.0**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

## 1. Introduction

"Building" refers to replacing placeholders on base16 _[template
files](./file.md)_ with colors from base16 _[schemes](./styling.md)_.

A template is a mustache file that acts as a "blueprint": it represents how to
output the scheme into other file formats, or (more commonly) how to output a
configuration file to theme a specific software. For example: a [vim
template](https://github.com/base16-project/base16-vim/blob/main/templates/default.mustache).

A scheme is a yaml file that represents a palette of 16 colors: to be replaced
on the placeholders the template files hold. For example: the [solarized
scheme](https://github.com/base16-project/base16-schemes/blob/main/solarized-dark.yaml)

A base16 builder is, essentially, an application that somehow implements the
_building_ feature specification: filling the placeholders on templates with
scheme colors.

Builders are categorized into:

- _reference tooling_: These follow the spec closely and are
  designed for unopinionated lower-level ("plumbing") usage, specifically for
  scripting and as component to build more complex base16 applications. High
  quality reference builders will usually be adopted by the base16-project
  organization;
- _extended tooling_: These are built for end users and are usually tailored
  for a usecase. This includes GUI apps, ergonomical CLI tools, scheme
  managers, web apps, and more. These apps are encouraged to use (or create)
  reference implementations as libraries, but may also implement the builder
  feature themselves. All of the following `MUST`s can be replaced by `SHOULD`s
  when writing this kind of tooling.

## 2. Template variables spec

A builder tool MUST provide the following variables, and no others, to the
template files it processes:

- `scheme-name` - obtained from the scheme file
- `scheme-author` - obtained from the scheme file
- `scheme-slug` - obtained from the scheme filename, as described above
- `scheme-kind` - either "light" or "dark", calculated from the `base00` color <!-- TODO: This is a candidate for inclusion, let me know your thoughts -->

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

## 3. Interface

All base16 reference builders MUST provide a single feature: building a
template using 1 or more schemes.

This section (`3`) is not relevant to extended tooling, which will have its own
interface fitting their intended usecases, altough they MAY expose the
reference CLI interface (through a `build` subcommand, for example) and/or a
library, if desired.

It is REQUIRED that this functionality is exposed by one (or both) of the following:

### 3.1. CLI

The binary name SHOULD contain `base16`, but is otherwise left as a choice to
the author.

To be fully compliant, a builder CLI interface MUST NOT include any other
feature, option, argument, or deviance from the expected interface and
behaviour of the program.

<!-- TODO: For convenience, we make a manpage and set of tests available. All
compliant builders MUST fully conform to these two. -->

The CLI interface MUST work without relying on any network connection.

#### 3.1.1 CLI Arguments and options

```bash
base16 <TEMPLATES-DIRECTORY> <SCHEME-FILE> ...
```

`TEMPLATES-DIRECTORY` being a directory containing a `config.yaml`, as well as at
least one `.mustache` template. These are usually named `templates` on all
base16 template repositories.

`SCHEME-FILE` being one or more `.yaml` scheme file. The main source for these
is the [base16-schemes](https://github.com/base16-project/base16-schemes)
repository.

The program MAY also offer the following options:

- `--debug | -d` option(s) for increasing log verbosity;
- `--version | -v` option to output its current running version;
- `--help | -h` option to output usage information directly or by opening the
  manpage.

These three options have output that is considered implementation detail, not
intended to be scripted with. Thus each author SHOULD implement them as they
see fit.

#### 3.1.2. CLI output and behaviour

**Note**: All text outputted by the CLI binary is considered implementation
detail, so the author MAY output whatever they prefer (or no message at all).
If needed, scripts using the builder SHOULD check for return codes (specified
below) instead of messages.

For all templates defined in the template config file (`config.yaml`, inside
the specified `TEMPLATES-DIRECTORY`), the builder MUST iterate through all the
specified schemes and output matching files.

The built filenames MUST be relative to the directory where the command is
executed, and MUST look like `<output-dir>/base16-<slug><extension>`, where the
`SLUG` is taken from the scheme filename made lowercase with spaces replaced
with dashes and both the extension and `output-dir` are taken from
`config.yaml`.

If the build fails for any reasons, the program MUST exit with code `1` and MAY
output an error message. This is not exhaustive and new exit codes might be
added in the future to account for specific errors, so scripters catching
generic errors SHOULD check for non-zero status.

Otherwise, the program MUST exit with code `0` and an OPTIONAL success message.

#### 3.1.3 CLI example:

```bash
git clone https://github.com/base16-project/base16-vim.git
git clone https://github.com/base16-project/base16-schemes.git
base16 base16-vim/templates base16-schemes/*.yaml
```

Should create a `colors` (on the current directory) containing `base16-XXX.vim`
files.

### 3.2. Library

The other option is exposing a software library other developers may use to
assist developing more complex base16-compatible tooling.

As above, the library MUST implement single feature: building templates.

This exposed library, or any internal code, has no specific required structure.

The author MAY choose how (through a class, function that operates on file
paths, etc) they will expose the builder functionality to the caller, according
to their judgement.

They SHOULD try to achieve an ergonomical and powerful interface and follow the
best practices on their respective programming languages.

Official reference implementations will follow semantic versioning matching
this spec, in the format: `<base16-version>-builder_revision`.

## 5. Considerations
Mustache was chosen as the templating language due to its simplicity and
widespread adoption across languages. YAML was chosen to describe scheme and
configuration files for the same reasons.

The core scheme repository was based off the single scheme repository so
builders supporting v0.8-v0.9 of the spec can continue to function without
changes.

The revised builder functionality specification introduced in v0.11 did not
introduce any changes to schemes or templates, so no changes to these are
needed. Older builders will continue to work, but authors are encouraged to
implement the new, simpler and more consistent, specification.
