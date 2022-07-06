# Styling Guidelines
**Version 0.3-dev**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

The colors for the default Base16 scheme were chosen to be pleasing and visualy distinctive,  but scheme designers may chose whichever colours they desire, e.g. `base0B` (green in the default scheme) might be swapped for yellow. Base16 (by default) groups similar language constructs within a single color. For example numbers (such as floats, ints, and doubles) would all belong to the same colour group (`base09`).

Describing syntax highlighting can be tricky - please see [base16-vim](https://github.com/base16-project/base16-vim/) and [base16-emacs](https://github.com/base16-project/base16-emacs/) for some real-life examples. It should be noted that each editor will have it's own idiosyncrasies due to having different syntax highlighting engines.

**Guidelines**

- Colors `base00` to `base07` are typically variations of a single hue and run from darkest to lightest. These colors are used for foreground and background, status bars, line highlighting and such.
- Colors `base08` to `base0F` are typically individual acddent colors used for syntax highlighting (types, operators, classes, variables, etc.)
- To create a dark scheme, colors `base00` to `base07` should span from darkest to lightest.
  - For a light scheme, these colours should span from lightest to darkest.

### Classic Schemes

Classic schemes specify only the original 16 base colors.  The semantic meaning of each base color (when syntax highighlighting) is listed below.

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

Extended themes MAY specify additional aliases that will override the original base colors.  For example if you didn't want "variables" and "xml tags" to use the same color (`base08`) you would use the aliase `name_variable` or `xml_tag` to specify a different color.


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

Aliases may refer to base colors (`baseXX`), literal hex color values, or even other aliases.

An example:

 ```yaml
base05: "ff0000"         # red
name_variable: "ff0000"  # red
constant: "base05"       # more red
string: "constant"         # still red
```

- `base05` refers to the hex color red
- `name_variable` refers to the hex color red
- `constant` refers to `base05`, which itself refers to red.
- `string` refers to `constant`, which refers to `base05`, which finally refers to red (`#ff0000`).


### Custom Aliases

You may also define custom alises to make your scheme easier to author/maintain. For example, it may be helpful to use custom aliases to describe your hues:

```yaml
super_vibrant_purple: "ee00ee"
red: "ff0000"
blue: "0000ff"
green: "00ff00"
base0b: super_vibrant_purple
base0c: red
base0d: blue
base0e: green
```

## Notes

### You may still use only 16 colors.

The number of colors per scheme is still limited to 16.  If you (via aliases) use more than 16 unique hex colors an error will be thrown during the build process.
