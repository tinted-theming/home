# ![Base16](logo.png)

An architecture for building themes based on carefully chosen syntax
highlighting using a base of sixteen colors.

It allows users to choose a color scheme they know will be available for all
their applications (both GUIs and terminal applications).

It allows color scheme designers to select a palette of 16 colors once and then
instantly generate theme files for many different applications.

See the [List of supported programs](#template-repositories) on how to apply
base16 themes on your favorate program.

## Gallery

We currently host 200+ color palletes. You can check out them at [Base16 Gallery](https://base16-project.github.io/base16-gallery).

## Documentation and Specification

Base16 provides a set of guidelines detailing how to style syntax and how to
code a _builder_ for compiling Base16 _schemes_ and _templates_.

### Scheme

A scheme is a list of 16 colors to be used as a base to build themes. To make
base16 look consistent, each color will be used for similar purpose in different
programs. See [Styling Guidelines](/styling.md) for more information on how each
color should be used.

A scheme is defined using a yaml file. The file specification is in
[File Guidelines](/file.md#scheme-files)

### Builder

A builder is a build tool used by various template repositories to generate
files based on scheme file and template file.

[Builder Guidelines](/builder.md)

### Template

A template defines how theme file(s) should be generated for a specific program.

It is typically installed directly by end user to use different base16 themes.

A template repository typically defines a template file, then uses a builder to
generate program specific theme files with the template file.

A template file will be used by builder to generate them.
The file specification is in [Template section in File Guidelines](/file.md#template-config-files)

## Template Repositories

To add your own template, submit a pull request to this repository to add your
repository to the "Unofficial Templates" list below in the relevant category.
**Recommended repository naming scheme: base16-[template-name]** (with dashes as
separators).

### Official Templates

As a part of the Base16 Project, we maintain a number of templates. Each has
been sponsored by at least one base16 project member who is committed to
maintaining that template.

We are open to accepting new projects, though they must still be sponsored by a
base16 project member and have some level of activity.

* [Emacs](https://github.com/base16-project/base16-emacs) maintained by [belak](https://github.com/belak)
* [FZF](https://github.com/base16-project/base16-fzf) maintained by [fnune](https://github.com/fnune)
* [Shell](https://github.com/base16-project/base16-shell) maintained by [belak](https://github.com/belak), [fnune](https://github.com/fnune), and [JamyGolden](https://github.com/JamyGolden)
* [TextMate/Sublime](https://github.com/base16-project/base16-textmate) maintained by [JamyGolden](https://github.com/JamyGolden)
* [Vim](https://github.com/base16-project/base16-vim) maintained by [fnune](https://github.com/fnune), [BonaBeavis](https://github.com/BonaBeavis), and [JamyGolden](https://github.com/JamyGolden)

### Contrib Templates

In order to prevent ownership issues, we're introducing the concept of contrib
templates. These are templates which have been handed over to the
base16-project, but either aren't sponsored by a base16-project member or don't
have enough usage to warrent including with our official templates.

Submitting a repository to [base16-project-contrib](https://github.com/base16-project-contrib)
and continuing to work on it is a great way to get involved and get noticed as a
maintainer so you can work towards getting added to the base16-project team.

### Unofficial Templates

If you have a template you maintain, but don't want to submit it to the contrib
repositories, feel free to add a link to the repository here to add it to this
list. These are community maintained templates and may not be updated often.

<details><summary><b>Terminals</b> - terminal and shell related templates</summary>
<p>

* [Alacritty](https://github.com/aarowill/base16-alacritty) maintained by [aarowill](https://github.com/aarowill)
* [Blink](https://github.com/niklaas/base16-blink) maintained by [niklaas](https://github.com/niklaas)
* [ConCfg](https://github.com/h404bi/base16-concfg) maintained by [h404bi](https://github.com/h404bi)
* [ConEmu](https://github.com/martinlindhe/base16-conemu) maintained by [martinlindhe](https://github.com/martinlindhe)
* [Console2](https://github.com/AFulgens/base16-console2) maintained by [AFulgens](https://github.com/AFulgens)
* [ConsoleZ](https://github.com/AFulgens/base16-consolez) maintained by [AFulgens](https://github.com/AFulgens)
* [Crosh](https://github.com/philj56/base16-crosh) maintained by [philj56](https://github.com/philj56)
* [fish](https://github.com/tomyun/base16-fish) maintained by [tomyun](https://github.com/tomyun)
* [fish-shell](https://github.com/FabioAntunes/base16-fish-shell) maintained by [FabioAntunes](https://github.com/FabioAntunes)
* [Gnome Terminal](https://github.com/aarowill/base16-gnome-terminal) maintained by [aarowill](https://github.com/aarowill)
* [iTerm2](https://github.com/martinlindhe/base16-iterm2) maintained by [martinlindhe](https://github.com/martinlindhe)
* [kermit](https://github.com/orhun/base16-kermit) maintained by [orhun](https://github.com/orhun)
* [kitty](https://github.com/kdrag0n/base16-kitty) maintained by [kdrag0n](https://github.com/kdrag0n)
* [Konsole](https://github.com/cskeeters/base16-konsole) maintained by [cskeeters](https://github.com/cskeeters)
* [MinTTY](https://github.com/geoffstokes/base16-mintty) maintained by [geoffstokes](https://github.com/geoffstokes)
* [PuTTY](https://github.com/benjojo/base-16-putty) maintained by [benjojo](https://github.com/benjojo)
* [st](https://github.com/honza/base16-st) maintained by [honza](https://github.com/honza)
* [Termite](https://github.com/khamer/base16-termite) maintained by [khamer](https://github.com/khamer)
* [Termux](https://github.com/kdrag0n/base16-termux) maintained by [kdrag0n](https://github.com/kdrag0n)
* [Tilix](https://github.com/karlding/base16-tilix) maintained by [karlding](https://github.com/karlding)
* [Windows Terminal](https://github.com/wuqs-net/base16-windows-terminal) maintained by [wuqs-net](https://github.com/wuqs-net)
* [XFCE4 Terminal](https://github.com/afq984/base16-xfce4-terminal) maintained by [afq984](https://github.com/afq984)
* [Xshell](https://github.com/h404bi/base16-xshell) maintained by [h404bi](https://github.com/h404bi)
* [Xresources](https://github.com/binaryplease/base16-xresources) maintained by [binaryplease](https://github.com/binaryplease)

</p>
</details>

<details><summary><b>Editors</b> - templates for use in code editors and IDEs</summary>
<p>

* [Frescobaldi](https://github.com/rkubosz/base16-frescobaldi) maintained by [rkubosz](https://github.com/rkubosz)
* [Godot](https://github.com/Calinou/base16-godot) maintained by [Calinou](https://github.com/Calinou)
* [gtksourceview3](https://github.com/GarkGarcia/base16-gtksourceview3) maintained by [GarkGarcia](https://github.com/GarkGarcia)
* [Jetbrains](https://github.com/adilosa/base16-jetbrains) maintained by [adilosa](https://github.com/adilosa)
* [Jetbrains IDE](https://github.com/ShiromMakkad/base16-jetbrains-ide) maintained by [ShiromMakkad](https://github.com/ShiromMakkad)
* [JOE](https://github.com/jjjordan/base16-joe) maintained by [jjjordan](https://github.com/jjjordan)
* [Kakoune](https://github.com/leira/base16-kakoune) maintained by [leira](https://github.com/leira)
* [MonoDevelop](https://github.com/netpyoung/base16-monodevelop) maintained by [netpyoung](https://github.com/netpyoung)
* [QOwnNotes](https://github.com/themix-project/base16-template-qOwnNotes) maintained by [themix-project](https://github.com/themix-project)
* [Scide](https://github.com/brunoro/base16-scide) maintained by [brunoro](https://github.com/brunoro)
* [Textadept](https://github.com/rgieseke/base16-textadept) maintained by [rgieseke](https://github.com/rgieseke)
* [TextMate & Sublime Text](https://github.com/chriskempson/base16-textmate) maintained by [chriskempson](https://github.com/chriskempson)
* [Vim-airline](https://github.com/dawikur/base16-vim-airline-themes) maintained by [dawikur](https://github.com/dawikur)
* [Vis](https://github.com/pshevtsov/base16-vis) maintained by [pshevtsov](https://github.com/pshevtsov)
* [vtrgb](https://github.com/coderonline/base16-vtrgb) maintained by [coderonline](https://github.com/coderonline)
* [VSCode](https://github.com/golf1052/base16-vscode) maintained by [golf1052](https://github.com/golf1052)
* [Xcode](https://github.com/kreeger/base16-xcode) maintained by [kreeger](https://github.com/kreeger)
* [ZOC Terminal](https://github.com/balthild/base16-zoc) maintained by [Balthild](https://github.com/balthild)

</p>
</details>

<details><summary><b>Window Managers</b> - window managers and related utilities</summary>
<p>

* [Dunst](https://github.com/khamer/base16-dunst) maintained by [khamer](https://github.com/khamer)
* [i3](https://github.com/khamer/base16-i3) maintained by [khamer](https://github.com/khamer)
  * [i3status](https://github.com/Eluminae/base16-i3status) maintained by [Eluminae](https://github.com/Eluminae)
  * [i3status-rust](https://github.com/mystfox/base16-i3status-rust) maintained by [mystfox](https://github.com/mystfox)
* [mako](https://github.com/Eluminae/base16-mako) maintained by [Eluminae](https://github.com/Eluminae)
* [Polybar](https://github.com/Misterio77/base16-polybar) maintained by [Misterio77](https://github.com/Misterio77)
* [qt5ct](https://github.com/mnussbaum/base16-qt5ct) maintained by [mnussbaum](https://github.com/mnussbaum)
* [Rofi](https://gitlab.com/jordiorlando/base16-rofi) maintained by [jordiorlando](https://gitlab.com/jordiorlando)
* [StumpWM](https://github.com/tpine/base16-stumpwm) maintained by [tpine](https://github.com/tpine)
* [Sway](https://github.com/rkubosz/base16-sway) maintained by [rkubosz](https://github.com/rkubosz)
* [Swaylock](https://git.michaelball.name/gid/base16-swaylock-template) maintained by [michael-ball](https://git.michaelball.name)
* [Waybar](https://github.com/mnussbaum/base16-waybar) maintained by [mnussbaum](https://github.com/mnussbaum)
* [Window Maker](https://github.com/d-torrance/base16-wmaker) maintained by [d-torrance](https://github.com/d-torrance)
* [Wofi](https://sr.ht/~knezi/base16-wofi) maintained by [knezi](https://sr.ht/~knezi)
* [Wofi colors file](https://github.com/agausmann/base16-wofi-colors) maintained by [agausmann](https://github.com/agausmann)

</p>
</details>

<details><summary><b>Programming</b> - defaults and utils for use when programming</summary>
<p>

* [Binary Ninja](https://github.com/evanrichter/base16-binary-ninja) maintained by [evanrichter](https://github.com/evanrichter)
* [C Header](https://github.com/m1sports20/base16-c_header) maintained by [m1sports20](https://github.com/m1sports20)
* [CSS, Less, Sass/Scss & Stylus](https://github.com/samme/base16-styles) maintained by [samme](https://github.com/samme)
* [GTK+ FlatColor](https://github.com/Misterio77/base16-gtk-flatcolor) maintained by [Misterio77](https://github.com/Misterio77)
* [GTK+2](https://github.com/dawikur/base16-gtk2) maintained by [dawikur](https://github.com/dawikur)
* [Highlight](https://github.com/bezhermoso/base16-highlight) maintained by [bezhermoso](https://github.com/bezhermoso)
* [Highlight.js](https://github.com/highlightjs/base16-highlightjs) maintained by [joshgoebel](https://github.com/joshgoebel)
* [HTML Previews](https://github.com/chriskempson/base16-html-preview) maintained by [chriskempson](https://github.com/chriskempson)
* [Prism](https://github.com/atelierbram/base16-prism) maintained by [atelierbram](https://github.com/atelierbram)
* [prompt-toolkit & ipython](https://github.com/memeplex/base16-prompt-toolkit) maintained by [memeplex](https://github.com/memeplex)
* [Pygments](https://github.com/mohd-akram/base16-pygments) maintained by [mohd-akram](https://github.com/mohd-akram)
* [Qt Creator](https://github.com/ilpianista/base16-qtcreator) maintained by [ilpianista](https://github.com/ilpianista)

</p>
</details>

<details><summary><b>Other</b> - various applications which don't fit in other categories</summary>
<p>

* [Amfora](https://github.com/jo1gi/base16-amfora) maintained by [jo1gi](https://github.com/jo1gi)
* [HexChat](https://github.com/Diablo-D3/base16-hexchat) maintained by [Diablo-D3](https://github.com/Diablo-D3)
* [LuaKit](https://github.com/twnaing/base16-luakit) maintained by [twnaing](https://github.com/twnaing)
* [qutebrowser](https://github.com/theova/base16-qutebrowser) maintaned by [theova](https://github.com/theova)
* [Vimiv](https://github.com/karlch/base16-vimiv) maintained by [karlch](https://github.com/karlch)
* [zathura](https://github.com/HaoZeke/base16-zathura) maintained by [HaoZeke](https://github.com/HaoZeke)
* [Windows Command Prompt](https://github.com/iamthad/base16-windows-command-prompt) maintained by [iamthad](https://github.com/iamthad)

</p>
</details>

## Schemes

To add your own scheme, submit a pull request to the [base16-schemes repo](https://github.com/base16-project/base16-schemes) and add your scheme.

## Builders

Normally end-users should not need to use builders, as they're primarily meant
for maintainers - both scheme and template maintainers. These are tools used to
build templates with all the currently submitted schemes.

### Official Builder Repositories

Similar to our split between official and unofficial templates, we also have a
similar split for builders. Spec changes will not be merged until there is
consensus among maintainers and at least one builder with a pull request ready
for implementing that spec version.

* [Base 16 Builder Go](https://github.com/base16-project/base16-builder-go) maintained by [belak](https://github.com/belak) - currently supports 0.10.0
* [Base16 Builder Node](https://github.com/base16-project/base16-builder-node) maintained by [JoshGoebel](https://github.com/JoshGoebel) - currently supports 0.9.1

### Unofficial Builder Repositories

**Repository naming scheme: base16-builder-[language]** (with dashes as separators). The separate headings are the latest versions of the spec supported by each builder.

### Changelog

#### 0.10.0 (Mar 20, 2021)

- Simplify repo structure and builder responsibilities
- Clarify that using a hash as a part of the color is allowed

#### 0.9.1 (Jun 15, 2019)

- Make baseXX-hex-bgr variables available to templates
- Warn when a template file has been overwritten

* [Base 16 Builder Ansible](https://github.com/mnussbaum/base16-builder-ansible) maintained by [mnussbaum](https://github.com/mnussbaum)
* [Base 16 Builder PHP](https://github.com/chriskempson/base16-builder-php) maintained by [chriskempson](https://github.com/chriskempson)
* [Base 16 Builder Python](https://github.com/InspectorMustache/base16-builder-python) maintained by [InspectorMustache](https://github.com/InspectorMustache)
* [Base 16 Builder Rust](https://github.com/ilpianista/base16-builder-rust) maintained by [ilpianista](https://github.com/ilpianista)

#### 0.9.0 (Jul 6, 2017)

- Add decimal color variables

* [Base 16 Builder Clojure](https://github.com/nhurden/base16-builder-clojure) maintained by [nhurden](https://github.com/nhurden)
* [Base 16 Builder Elixir](https://github.com/obahareth/base16-builder-elixir) maintained by [obahareth](https://github.com/obahareth)
* [Base 16 Builder Ruby](https://github.com/obahareth/base16-builder-ruby) maintained by [obahareth](https://github.com/obahareth)
* [Base 16 Builder Typescript](https://github.com/golf1052/base16-builder-typescript) maintained by [golf1052](https://github.com/golf1052)

#### 0.8.1 (Dec 29, 2016)

- Clarify theme filename generation
- Various clarifications

* [Base 16 Builder Perl](https://github.com/loomer/base16-builder-perl) maintained by [loomer](https://github.com/loomer)

#### 0.8.0 (Aug 27, 2016)

- Drop support for HSL variables

## Scheme and Template Author Resources

The following is a list of useful resources for anyone creating a Base16 scheme and or template:

* [Code Examples](https://github.com/chriskempson/base16-code-examples) - A list of example code file for various languages.
* [TmTheme Editor](http://tmtheme-editor.herokuapp.com) - An online editor for themes in tmTheme format.
* [Base16 Template Converter](https://github.com/ntpeters/base16-template-converter) - A script to automatically convert Base16 templates written in the old Embedded Ruby style to the new Mustache style.

## Tools for using Base16

If you've written a tool for base16 feel free to add it to the list below:

* [auto-base16-theme](https://github.com/makuto/auto-base16-theme) - A command line tool to create a base16 theme from an input image's color palette.
* [base16-manager](https://github.com/AuditeMarlow/base16-manager) - A command line tool to install base16 templates and set themes globally.
* [base16-shell-preview](https://github.com/nvllsvm/base16-shell-preview) - A command line tool to preview and set base16-shell themes.
* [base16-universal-manager](https://github.com/binaryplease/base16-universal-manager) - A command line tool to automatically get, build and set base16 themes globally for *all* supported applications. Themes and templates are pulled form the official repositories or from a local cache.
* [flavours](https://github.com/misterio77/flavours) - A command line tool to manage and globally apply base16 templates by specifying a scheme name.
* [Themix/Oomox](https://github.com/themix-project/oomox/) - Graphical application for generating different color variations of a Arc, Materia and Oomox themes (GTK2, GTK3 and others), Archdroid, Gnome-Colors and Numix icons, and terminal palette. Base16 plugin allows to open Base16 YAML files a export both Base16 and its own themes using Base16 Mustache templates.
* [base16-spectrum-generator](https://github.com/alexmirrington/base16-spectrum-generator) - A Python script for generating `.png` files showcasing the colours in a base16 theme.
* [base16.nix](https://github.com/SenchoPens/base16.nix) - a NixOS / home-manager module to set base16 / base24 schemes and use templates.

## Projects using Base16

* [Visual Studio Code](https://code.visualstudio.com) - Code Editor
* [Atom Editor](https://atom.io) - Code Editor
* [c-Tiles16](https://github.com/atelierbram/c-tiles16) - Colorscheming with Variables.
* [Spacegray](https://github.com/kkga/spacegray) - A set of custom UI themes for Sublime Text 2/3.
* [Harmonic16](http://janniks.github.io/harmonic16) - A color generator for harmonic Base16 color-schemes.
* [Duotone-base16](https://github.com/davidosomething/duotone-base16) - A Duotone scheme to Base16 convertor.
* [terminal.sexy](https://terminal.sexy) - Terminal Color Scheme Designer
* [Just-Colors](https://github.com/andreyvpng/just-colors) - Simple configuration file generator
* [Highlight.js](https://highlightjs.org) - JavaScript syntax highlighter
* [nix-colors](https://github.com/Misterio77/nix-colors) - Designed to help with Nix(OS) theming.

## Non-template Base16 Themes

* [base16-mutt](https://github.com/josephholsten/base16-mutt) - a config file for mutt which uses base16 colors from the terminal

## Credits

Thanks to [Chris Kempson](https://github.com/chriskempson) for the original concept and implementation.
