# All your themes, everywhere.

Style systems and smart build tooling for crafting high fidelity color schemes and easily using them in all your favorite apps.

**Features**

- Seamless builder support for _multiple_ style systems ([Base16](https://github.com/chriskempson/base16), [Base17](https://github.com/base16-project/base17), [Base24](https://github.com/Base24/base24/), [BaseNext](https://github.com/base16-project/basenext), etc.)
- Over 230 beautiful and ready-to-use color schemes. [View the Gallery](https://base16-project.github.io/base16-gallery).
- Over 70 supported GUI and terminal applications. [See the full list](#supported-applications).
- Allows end users to choose a color scheme and know it will be available _everywhere_.
- Allows color scheme designers to craft a palette of colors once, instantly supporting for many different apps.

## Documentation and Specification

Each _style system_ details which color tokens it provides to the _builder_, while the _builder_ spec details which variables are provided to _templates_ during the _building_ process.

### Scheme

A scheme is a fixed palette of named colors and (optionally) instructions for how those colors should be used by apps.

### Style Systems

A style guide provides rules governing how a scheme's palette should be applied within apps.  This means each color is used consistently for similar purposes across all your apps.  Individual styling guides often support different sized pallets and have different ideas about how those colors should be deployed.

See the individual styling guides for more information on each:

- [Base17](https://github.com/base16-project/base17) - our fork of Base16. It still has 16 colors, but aims to make incremental improvements to the system.
- [BaseNext](https://github.com/base16-project/basenext) - more complexity, but also far more power and flexibility to create higher fidelity themes and templates.
- [Base24](https://github.com/Base24/base24/blob/master/styling.md) - an extra 8 colors for full ANSI support in your terminals.

A scheme is defined using a [YAML](https://yaml.org/) file. The file specification is in the [Builder Guidelines](/builder.md#schemes-repository).


### Builder

A builder is a build tool used by various template repositories to generate files based on scheme file and template file.

- [Builder Guidelines](/builder.md)

### Template

A template describes how a scheme should be transformed to support a specific application.  A template repository defines template files, then uses a builder to generate application specific files using the templates.

Template repositories often include pre-built versions of every scheme to make it easier to use. These are typically installed directly by end users to use the schemes in different applications.

## Builders

Normally end-users should not need to use builders, as they're primarily meant for maintainers - both scheme and template maintainers. These are tools used to build templates for different scheme systems.

Spec changes will not be released until there is consensus among maintainers and at least one builder with a pull request ready for implementing that spec version.

See the [CHANGELOG](/CHANGELOG.md) for more information about changes in the
spec.

* [Base16 Builder Go](https://github.com/base16-project/base16-builder-go) maintained by [belak](https://github.com/belak) - currently supports 0.10.0
* [Base16 Builder Node](https://github.com/base16-project/base16-builder-node) maintained by [joshgoebel](https://github.com/joshgoebel) - currently supports 0.10.0

## Projects

These are projects which may not be directly related to Base16 Project, but are still theming related.

* [terminal.sexy](https://terminal.sexy) - Terminal Color Scheme Designer
* [Just-Colors](https://github.com/andreyvpng/just-colors) - Simple configuration file generator
* [Highlight.js](https://highlightjs.org) - JavaScript syntax highlighter
* [nix-colors](https://github.com/Misterio77/nix-colors) - Designed to help with Nix(OS) theming.
* [TmTheme Editor](http://tmtheme-editor.herokuapp.com) - An online editor for themes in tmTheme format. This is a useful resource for anyone creating a scheme and/or template.

## Project Chat

Have something you want to discuss, but you're not sure it warrants an issue? Feel free to stop by the [#base16 channel](https://web.libera.chat/#base16) on [Libera Chat](https://libera.chat/) or the [bridged Matrix channel](https://matrix.to/#/#base16:libera.chat) to talk about it.

## Credits

- Thanks to [Chris Kempson](https://github.com/chriskempson) for the original concept and implementation.
