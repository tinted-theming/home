# Base17 Style & Scheme Guide

**Version 0.9.1-beta**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

<!-- MarkdownTOC levels="2,3,4" autolink="true" -->

- [The Palette](#the-palette)
- [The Default Slots](#the-default-slots)
  - [Customize Syntax Highlighting](#customize-syntax-highlighting)
  - [Customizing Syntax Highlighting](#customizing-syntax-highlighting)
  - [Slot Values](#slot-values)
  - [Variable Slots](#variable-slots)
- [Addendums](#addendums)
  - [You are still limited to a max of 16 colors.](#you-are-still-limited-to-a-max-of-16-colors)
  - [Issues that Base17 attempts to solve](#issues-that-base17-attempts-to-solve)
    - [Sameness](#sameness)
    - [Semantic Pairing](#semantic-pairing)
- [Examples](#examples)
  - [skittles.yaml](#skittlesyaml)

<!-- /MarkdownTOC -->

## The Palette

The Base17 palette consists of an 8 shade gradient ramp for foreground/background/UI plus 8 accent colors for syntax highlighting.  The eight accent colors for a Base17 scheme should strive to be pleasing and visualy distinctive. Designers may chose any accent colours they desire - in any order. Slots in the palette _purposely_ do not correspond to particular hues. The same hues across many themes results in [sameness](#sameness).

By default, similar language constructs are assigned to a single color "slot". For example literals (numbers, booleans, etc) by default are assigned to slot `base09`.

Describing syntax highlighting can be tricky - please see [base16-vim](https://github.com/base16-project/base16-vim/) and [base16-emacs](https://github.com/base16-project/base16-emacs/) for some real-life examples. It should be noted that each editor will have it's own idiosyncrasies due to having different syntax highlighting engines.

**Compatibility**

Base17 is an evolution of [Base16 v0.2 spec](https://github.com/chriskempson/base16/blob/main/styling.md).  It still includes 16 colors.

- All Base16 v0.2 schemes are forwards compatible with Base17.
  - _Every Base16 scheme is a fully valid Base17 scheme._
- Base17 schemes may not be backwards compatible with Base16.

To upgrade a scheme from Base16 just start using Base17 features then build using a Base17 aware builder.


**Guidelines**

- Slots `base00` to `base07` typically capture a wide gradient of a single hue. These slots are used for foreground and background, status bars, line highlighting and such.
	- For a dark scheme, these slots typically span from darkest to lightest. (`base00` is the darkest)
	- For a light scheme, these slots typically span from lightest to darkest. (`base00` is the lightest)
- Slots `base08` to `base0F` typically hold individual accent colors used for syntax highlighting (types, operators, classes, variables, etc.)


## The Default Slots

The default slots, their intended usage, and the built-in slots they fill by default.


| Slot       | Usage  | Fills slot by default... |
| :-- | :-- | :-- |
| _base00_ | Default Background  | `background` |
| _base01_ | Lighter Background | `bg_lighter`, `folding_marks`, `line_numbers` |
| _base03_ | Comments, Invisibles, Line Highlighting | `bg_brightest`, `comment`, `invisible`, `line_highlighting` |
| _base04_ | Dark Foreground (Used for status bars) | `fg_darker`, `dark_status_bar` |
| _base05_ | Default Foreground, Caret, Delimiters, Operators | `foreground`, `caret`, `delimiter`, `operator` |
| _base06_ | Light Foreground | `fg_lighter` |
| _base07_ | Lightest Foreground | `fg_brightest` |
| _base08_ | Variables, XML Tags, Markup Link Text, Markup Lists, Diff Deleted| `variable`, `xml_tag`, `markup_link_text`, `markup_list`, `diff_deleted` |
| _base09_ | Integers, Boolean, Constants, XML Attributes, Markup Link Url| `literal`, `constant`, `xml_attribute`, `markup_link_url` |
| _base0A_ | Classes, Markup Bold, Search Text Background| `name_class`, `markup_bold` `bg_search_text` |
| _base0B_ | Strings, Inherited Class, Markup Code, Diff Inserted| `string`, `name_class_inherited`, `markup_code`, `diff_inserted` |
| _base0C_ | Support, Regular Expressions, Escape Characters, Markup Quotes| `support`, `regex`, `escape`, `markup_quotes` |
| _base0D_ | Functions, Methods, Attribute IDs, Headings| `function`, `attribute_id`, `heading` |
| _base0E_ | Keywords, Storage, Selector, Markup Italic, Diff Changed| `keyword`, `storage`, `selector`, `markup_italic`, `diff_changed` |
| _base0F_ | Deprecated, Opening/Closing Embedded Language Tags, e.g. `<?php ?>` | `deprecated`, `embed_tags` |

<!--
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

-->

**Note:**

- every scheme MUST assign all default Base slots
- older templates may only support the default slots (named slots will be ignored)
- variable slots may always be used to organize your scheme (even with older templates)


### Customize Syntax Highlighting

**Don't let a single use case for a slot dictate that slots color.**

Notice that `base08` by default fills `diff_deleted`.  Red is a popular shade for deletions.  Perhaps you're tempted to make `base08` red.  Pause first and ask: _Do you ALSO want variables, XML tags, markup link text, and markup lists to be red as well?_  Often the answer is _no_.

This problem is easily solved:

```yaml
# assuming we've defined $blue and $red variables
base08: $blue
diff_deleted: $red
```

Now _only deleted diffs will appear red_, the other uses of base08 will be blue.


<!--
### Customizing Syntax Highlighting

Schemes MAY customize highlighting to precisely fine tune how their palette will be applied inside applications.  For example if you don't desire variable names and xml tags to share the same coloration (slot `base08`) then you can use the `name_variable` and `xml_tag` built-in slots to specify different colors.
-->

<!--

**Foreground / Background**

- `background` - `base00` by default
- `bg_lighter` - `base01` by default
- `bg_????` - `base02` by default
- `bg_brightest` - `base03` by default
- `fg_darker` - `base04` by default
- `foreground` - `base05` by default
- `fg_lighter` - `base06` by default
- `fg_brightest` - `base07` by default


**UI**

- `bg_selection` - `base02` by default
- `bg_line_highlight` - `base03` by default
- `bg_search_text` - `base0A` by default
- `dark_status_bar` - `base04` by default
- `light_status_bar` - `base01` by default
- `caret` - `base05` by default
- `folding_marks` - `base01` by default

**Diff**

- `diff_inserted` - `base0B` by default
- `diff_changed` - `base0E` by default
- `diff_deleted` - `base08` by default

**Markup**

- `markup_link_text` - `base08` by default
- `markup_link_url` - `base09` by default
- `markup_list` - `base08` by default
- `markup_code` - `base0B` by default
- `markup_italic` - `base0E` by default
- `markup_bold` - `base0A` by default
- `markup_quoted` - `base0C` by default

**Editor / Source**

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

-->

### Slot Values

The value of a slot may be a literal hex color value or a reference to another slot.

 ```yaml
$red: "#ff0000"

constant: $red
string: "constant"
number: "constant"
boolean: "constant"
diff_deleted: $red

base05: "#fe0000"
```

- first we label the color `$red` with a variable
  - it's value is the literal color `#ff0000`
- we declare constants are red
- we declare strings, numbers, and booleans should be highlighted as constants
- we declare `diff_deleted` should be highlighted as `$red`
- we set `base05` to the literal hex color "#fe0000"


Note: Ordering does not matter, you can refer to a slot before that slot has been defined.


### Variable Slots

Variable slots make schemes easier to author and maintain. For example when your hues are visually distinct it's often helpful to reference them in your scheme by name:

```yaml
scheme: "Fun Colors"
$lightsaber_purple: "#FE00EF"
$granny_smith_red: "#EE1122"
$mr_blue_sky: "#336699"
base0b: $lightsaber_purple
base0c: $granny_smith_red
base0d: $mr_blue_sky
```

- all variable slot names must start with `$`


## Addendums

### You are still limited to a max of 16 colors.

The number of colors per scheme is still limited to 16.  If your scheme uses more than 16 unique hex colors an error will be thrown during the build process.


### Issues that Base17 attempts to solve

Base16 is pretty darn awesome at what it's managed to accomplish, but it's not without it's issues.

#### Sameness

Too often Base16 hues [stick frustratingly close the default scheme hues](https://github.com/base16-project/base16/issues/10#issuecomment-1171593477).  We imagine this may be because many designers start with the default palette as a base. This could also be influenced by semantic pairing.  The end result: a lot of themes look visually similar and there is less diversity in Base16 schemes than you find in other theming ecosystems.

_Base17 has no default scheme and explicitly discourages designers from trying to hue match other themes._


#### Semantic Pairing

With Base16 `base08` is used for both variables and diff deleted.  If you want deleted lines in diffs to be colored red you're stuck with red variables also, nothing you can do.  [Base16 themes include a lot of red variables.](https://github.com/base16-project/base16/issues/10)  This also entirely breaks the fidelity of some themes (like Nord) that are ported from richer ecosystems without such restrictions.

_Base17 allows you to override any default pairings and easily define two colors._ Variables blue, diff deleted red, you got it.


## Examples

### skittles.yaml

```yaml
scheme: "Skittles (dark)"
author: "Josh Goebel"

variables: # skittles
  $lemon: "#D7CA04"
  $orange: "#EE641C"
  $grape: "#6D5473"
  $raspberry: "#05538B"
  $strawberry: "#9A1518"
  $green_apple: "#28B109"
  $pineapple_passion: "#0098CB"
  $stawberry_starfruit: "#DD7EB2"

# adjust the default highlighting just a bit
# make sure diff is always green/red
customize:
  diff_inserted: $green_apple
  diff_changed: fg_darker
  diff_deleted: $strawberry

default: # bg/fg/ui
  base00: "#1C2023" # ----
  base01: "#393F45" # ---
  base02: "#565E65" # --
  base03: "#747C84" # -
  base04: "#ADB3BA" # +
  base05: "#C7CCD1" # ++
  base06: "#DFE2E5" # +++
  base07: "#F3F4F5" # ++++
  # accents
  base08: $strawberry
  base09: $orange
  base0A: $lemon
  base0B: $green_apple
  base0C: $pineapple_passion
  base0D: $raspberry
  base0E: $strawberry_starfruit
  base0F: $grape
```
