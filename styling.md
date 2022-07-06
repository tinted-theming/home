# Base17 Style Guide

**Version 0.9.0-dev**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

The accent colors for the default Base17 scheme were chosen to be pleasing and visualy distinctive, but scheme designers may chose whichever colours they desire, e.g. `base0B` (green in default) might be swapped for yellow. By default similar language constructs are grouped within a single color "slot". For example numbers (floats, integers, etc.) by default are grouped into slot `base09`.

Describing syntax highlighting can be tricky - please see [base16-vim](https://github.com/base16-project/base16-vim/) and [base16-emacs](https://github.com/base16-project/base16-emacs/) for some real-life examples. It should be noted that each editor will have it's own idiosyncrasies due to having different syntax highlighting engines.

**Compatibility**

Base17 is an evolution of [Base16 v0.2 spec](https://github.com/chriskempson/base16/blob/main/styling.md).  It still includes 16 colors.

- All Base16 v0.2 schemes are forwards compatible with Base17.
  - _Every Base16 scheme is a fully valid Base17 scheme._
- Base17 schemes may not be backwards compatible with Base16.

To upgrade a scheme from Base16 just start using Base17 features in your scheme and build using a Base17 aware builder.


**Guidelines**

- Slots `base00` to `base07` typically capture a wide gradient of a single hue. These slots are used for foreground and background, status bars, line highlighting and such.
	- For a dark scheme, these slots typically span from darkest to lightest. (`base00` is the darkest)
	- For a light scheme, these slots typically span from lightest to darkest. (`base00` is the lightest)
- Slots `base08` to `base0F` typically hold individual accent colors used for syntax highlighting (types, operators, classes, variables, etc.)


### The Default Slots

The default slots, their intended usage, and the built-in slots they fill by default.  For example `background` defaults to `base00` if it is not explicitely specified by name.

- **base00** - Default Background
 - `background`
- **base01** - Lighter Background (Used for status bars, line number and folding marks)
  - `bg_lighter`, `folding_marks`
- **base02** - Selection Background
  - `bg_selection`, `bg_????`
- **base03** - Comments, Invisibles, Line Highlighting
	- `comment`, `invisible`, `line_highlighting`
- **base04** - Dark Foreground (Used for status bars)
  - `fg_darker`, `dark_status_bar`
- **base05** - Default Foreground, Caret, Delimiters, Operators
  - `foreground`, `caret`, `delimiter`, `operator`
- **base06** - Light Foreground
	- `fg_lighter`
- **base07** - Lightest Foreground
	- `fg_brightest`
- **base08** - Variables, XML Tags, Markup Link Text, Markup Lists, Diff Deleted
  - `variable`, `xml_tag`, `markup_link_text`, `markup_list`, `diff_deleted`
- **base09** - Integers, Boolean, Constants, XML Attributes, Markup Link Url
	- `literal`, `constant`, `xml_attribute`, `markup_link_url`
- **base0A** - Classes, Markup Bold, Search Text Background
  - `name_class`, `markup_bold` `bg_search_text`
- **base0B** - Strings, Inherited Class, Markup Code, Diff Inserted
  - `string`, `name_class_inherited`, `markup_code`, `diff_inserted`
- **base0C** - Support, Regular Expressions, Escape Characters, Markup Quotes
  - `support`, `regex`, `escape`, `markup_quotes`
- **base0D** - Functions, Methods, Attribute IDs, Headings
	- `function`, `attribute_id`, `heading`
- **base0E** - Keywords, Storage, Selector, Markup Italic, Diff Changed
	- `keyword`, `storage`, `selector`, `markup_italic`, `diff_changed`
- **base0F** - Deprecated, Opening/Closing Embedded Language Tags, e.g. `<?php ?>`

**Keep in Mind**

- every scheme MUST specify all default Base slots
- older templates may only support the default slots (ignoring any named slots)
- for convenience custom slots by always be used to organize your scheme


### Built-in Slots

Schemes MAY use built-in slots to precisely fine tune how their color palette will be applied in applications.  For example if you don't desite variable names and xml tags to share the same color (slot `base08`) then you can use the `name_variable` and `xml_tag` built-in slots to specify different colors.


#### Foreground / Background

- `background` - `base00` by default
- `bg_lighter` - `base01` by default
- `bg_????` - `base02` by default
- `bg_brightest` - `base03` by default
- `fg_darker` - `base04` by default
- `foreground` - `base05` by default
- `fg_lighter` - `base06` by default
- `fg_brightest` - `base07` by default


#### UI

- `bg_selection` - `base02` by default
- `bg_line_highlight` - `base03` by default
- `bg_search_text` - `base0A` by default
- `dark_status_bar` - `base04` by default
- `light_status_bar` - `base01` by default
- `caret` - `base05` by default
- `folding_marks` - `base01` by default

#### Diff

- `diff_inserted` - `base0B` by default
- `diff_changed` - `base0E` by default
- `diff_deleted` - `base08` by default

#### Markup

- `markup_link_text` - `base08` by default
- `markup_link_url` - `base09` by default
- `markup_list` - `base08` by default
- `markup_code` - `base0B` by default
- `markup_italic` - `base0E` by default
- `markup_bold` - `base0A` by default
- `markup_quoted` - `base0C` by default

#### Editor / Source

- `delimiter` - `base05` by default
- `operator` - `base05` by default
- `comment` - `base03` (as a FG color) by default
- `invisibles` - `base03` (as foreground) by default
- `name_class` - `base0A` by default
- `name_class_inherited` - `base0B` by default
- `name_function` - `base0D` by default
- `name_support` - `base0C` by default
- `name_variable` - `base08` by default
- `xml_tag` - `base08` by default
- `xml_attribute` - `base09` by default
- `embed_tag` - `base0F` by default
- `constant` - `base09` by default
- `number` - `base09` by default
- `boolean` - `base09` by default
- `string` - `base0B` by default
- `regex` - `base0C` by default
- `escape_chars` - `base0C` by default
- `attribute_id` - `base0D` by default
- `heading` - `base0D` by default
- `keyword` - `base0E` by default
- `storage` - `base0E` by default
- `selector` - `base0E` by default
- `deprecated` - `base0F` by default


### Slot Values

The value of any slot may be a literal hex color value or a reference to another slot.

An example:

 ```yaml
$red: "ff0000"
string: "constant"
constant: $red
number: "constant"
boolean: "constant"
base05: "ff0000"
diff_deleted: $red
```

All the above slots resolve to the color red.

- `string` refers to the slot `constant`
- `constant` refers to the variable slot `$red`
- `$red` refers to the literal hex color red, `#ff0000`
- `base05` refers to the literal hex color red
- `diff_deleted` also refers to the literal hex color red


Note: The ordering does not matter, you can refer to a slot before that slot has been defined.


### Variable Slots

Variable slots make schemes easier to author and maintain. For example if your hues are visually distinct it could be helpful to name them and reference them later by name:

```yaml
scheme: "Fun Colors"
$lightsaber_purple: "fe00ef"
$granny_smith_red: "ee1122"
$mr_blue_sky: "336699"
base0b: $lightsaber_purple
base0c: $granny_smith_red
base0d: $mr_blue_sky
```

- all variable slot names must start with `$`


## Notes

### You are still limited to a max of 16 colors.

The number of colors per scheme is still limited to 16.  If you (via slots) create more than 16 unique hex colors an error will be thrown during the build process.


## Examples

**skittles.yaml**

```yaml
scheme: "Skittles (dark)"
author: "Josh Goebel"

# skittle variables
$lemon: "#D7CA04"
$orange: "#EE641C"
$grape: "#6D5473"
$raspberry: "#05538B"
$strawberry: "#9A1518"
$green_apple: "#28B109"
$pineapple_passion: "#0098CB"
$stawberry_starfruit: "#DD7EB2"

# make sure diff is always green/red
diff_inserted: $green_apple
diff_changed: fg_darker
diff_deleted: $strawberry

# bg/fg/ui
base00: "#1C2023" # ----
base01: "#393F45" # ---
base02: "#565E65" # --
base03: "#747C84" # -
base04: "#ADB3BA" # +
base05: "#C7CCD1" # ++
base06: "#DFE2E5" # +++
base07: "#F3F4F5" # ++++

# accent colors
base08: $strawberry
base09: $orange
base0A: $lemon
base0B: $green_apple
base0C: $pineapple_passion
base0D: $raspberry
base0E: $strawberry_starfruit
base0F: $grape
```
