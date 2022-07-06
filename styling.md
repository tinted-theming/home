# Styling Guidelines
**Version 0.3-dev**

Base16 aims to group similar language constructs with a single color. For example, floats, ints, and doubles would belong to the same colour group. The colors for the default scheme were chosen to be easily separable, but scheme designers should pick whichever colours they desire, e.g. base0B (green by default) could be replaced with red. There are, however, some general guidelines below that stipulate which base0B should be used to highlight each construct when designing templates for editors.

Since describing syntax highlighting can be tricky, please see [base16-vim](https://github.com/base16-project/base16-vim/) and [base16-emacs](https://github.com/base16-project/base16-emacs/) for reference. Though it should be noted that each editor will have some discrepancies due the fact that editors generally have different syntax highlighting engines.

Colors base00 to base07 are typically variations of a shade and run from darkest to lightest. These colors are used for foreground and background, status bars, line highlighting and such. Colors base08 to base0F are typically individual colors used for types, operators, names and variables. In order to create a dark scheme, colors base00 to base07 should span from dark to light. For a light scheme, these colours should span from light to dark.

### Classic Schemes

Classic schemes MUST specify only the original 16 base colors.  The semantic meaning of each base color is listed below.

- **base00** - Default Background
- **base01** - Lighter Background (Used for status bars, line number and folding marks)
- **base02** - Selection Background
- **base03** - Comments, Invisibles, Line Highlighting
- **base04** - Dark Foreground (Used for status bars)
- **base05** - Default Foreground, Caret, Delimiters, Operators
- **base06** - Light Foreground (Not often used)
- **base07** - Light Background (Not often used)
- **base08** - Variables, XML Tags, Markup Link Text, Markup Lists, Diff Deleted
- **base09** - Integers, Boolean, Constants, XML Attributes, Markup Link Url
- **base0A** - Classes, Markup Bold, Search Text Background
- **base0B** - Strings, Inherited Class, Markup Code, Diff Inserted
- **base0C** - Support, Regular Expressions, Escape Characters, Markup Quotes
- **base0D** - Functions, Methods, Attribute IDs, Headings
- **base0E** - Keywords, Storage, Selector, Markup Italic, Diff Changed
- **base0F** - Deprecated, Opening/Closing Embedded Language Tags, e.g. `<?php ?>`

### Extended Schemes

Extended themes MAY specify additional context sensative aliases that when specified supercede the original base colors.  For example if you don't want "variables" and "xml tags" to both be the same color (`base08`) you can specify either (or both) as alises - and assign a different color.


#### Foreground / Background

- bg_default - `base00` by default
- bg_lighter - `base01` by default
- bg_???? - `base02` by default
- bg_???? - `base03` by default
- fg_darker - `base04` by default
- fg_default - `base05` by default
- fg_lighter - `base06` by default
- fg_very_light - `base07` by default


#### UI

- bg_selection - `base02` by default
- bg_line_highlight - `base03` by default
- bg_search_text - `base0A` by default
- dark_status_bar - `base04` by default
- light_status_bar - `base01` by default

#### Diff

- diff_inserted - `base0B` by default
- diff_changed - `base0E` by default
- diff_deleted - `base08` by default

#### Markup

- markup_link_text - `base08` by default
- markup_link_url - `base09` by default
- markup_list - `base08` by default
- markup_code - `base0B` by default
- markup_italic - `base0E` by default
- markup_bold - `base0A` by default
- markup_quoted - `base0C` by default

#### Source / Other

- caret - `base05` by default
- delimiters - `base05` by default
- operator - `base05` by default
- comments - `base03` (as a FG color) by default
- invisibles - `base03` (as foreground) by default
- name_class - `base0A` by default
- name_class_inherited - `base0B` by default
- name_function - `base0D` by default
- name_method  - `base0D` by default
- name_support - `base0C` by default
- name_variable  - `base08` by default
- xml_tag  - `base08` by default
- xml_attribute - `base09` by default
- embed_tag - `base0F` by default
- number - `base09` by default
- boolean - `base09` by default
- constant - `base09` by default
- string - `base0B` by default
- regex - - `base0C` by default
- escape_chars - `base0C` by default
- attribute_id - `base0D` by default
- heading - `base0D` by default
- keyword - `base0E` by default
- storage - `base0E` by default
- selector - `base0E` by default
- deprecated - `base0F` by default

### How to specify an alias

Aliases may refer to hex color values, base colors (`baseXX`), or even other aliases.

An example:

 ```yaml
base05: "ff0000" # red
name_variable: "ff0000" # red
constant: "base05"
string: "number"
```

- `base05` refers to the hex color red
- `name_variable` refers to the hex color red
- `constant` refers to `base05`, which itself refers to red.
- `string` refers to `constant`, which refers to `base05`, which again refers to red.


### Custom Aliases

You may also define custom alises to make your scheme easier to author/maintain. For example, it may be helpful to use custom aliases to describe your hues:

```yaml
red: "ff0000"
blue: "0000ff"
green: "00ff00"
base0c: red
base0d: blue
base0e: green
```

## Notes

### You may still only use 16 colors.

The number of colors per scheme is still limited to 16.  If you (via aliases) use more than 16 unique hex colors an error will be thrown during the build process.
