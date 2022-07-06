# Styling Guidelines
**Version 0.3-dev**

*The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).*

The colors for the default Base16 scheme were chosen to be pleasing and visualy distinctive,  but scheme designers may chose whichever colours they desire, e.g. `base0B` (green in the default scheme) might be swapped for yellow. Base16 (by default) groups similar language constructs within a single color. For example numbers (such as floats, ints, and doubles) would all belong to the same colour group (`base09`).

Describing syntax highlighting can be tricky - please see [base16-vim](https://github.com/base16-project/base16-vim/) and [base16-emacs](https://github.com/base16-project/base16-emacs/) for some real-life examples. It should be noted that each editor will have it's own idiosyncrasies due to having different syntax highlighting engines.

**Guidelines**

- Colors `base00` to `base07` are typically a wide gradient of a single hue. These colors are used for foreground and background, status bars, line highlighting and such.
	- For a dark scheme, these colors should span from darkest to lightest. (`base00` is the darkest)
	- For a light scheme, these colours should span from lightest to darkest. (`base00` is the lightest)
- Colors `base08` to `base0F` are typically individual acddent colors used for syntax highlighting (types, operators, classes, variables, etc.)

### Base16 - The Default "Base" 16 Slots

The default semantic meaning/mappings(s) of each slot (for syntax highighlighting) are listed below.

- **base00** - Default Background
- **base01** - Lighter Background (Used for status bars, line number and folding marks)
- **base02** - Selection Background
- **base03** - Comments, Invisibles, Line Highlighting
- **base04** - Dark Foreground (Used for status bars)
- **base05** - Default Foreground, Caret, Delimiters, Operators
- **base06** - Light Foreground
- **base07** - Lightest Foreground
- **base08** - Variables, XML Tags, Markup Link Text, Markup Lists, Diff Deleted
- **base09** - Integers, Boolean, Constants, XML Attributes, Markup Link Url
- **base0A** - Classes, Markup Bold, Search Text Background
- **base0B** - Strings, Inherited Class, Markup Code, Diff Inserted
- **base0C** - Support, Regular Expressions, Escape Characters, Markup Quotes
- **base0D** - Functions, Methods, Attribute IDs, Headings
- **base0E** - Keywords, Storage, Selector, Markup Italic, Diff Changed
- **base0F** - Deprecated, Opening/Closing Embedded Language Tags, e.g. `<?php ?>`

### Named Slots (Aliases)

Schemes MAY use additional named slots (aliases) to override individual base slot mappings.  For example if you don't want variables and xml tags to use the same color (`base08`): use the `name_variable` and `xml_tag` slots to specify different colors.


#### Foreground / Background

- background - `base00` by default
- bg_lighter - `base01` by default
- bg_???? - `base02` by default
- bg_???? - `base03` by default
- fg_darker - `base04` by default
- foreground - `base05` by default
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

The value a given color may refer to a literal hex color value, another base colors (`baseXX`), or even another alias.

An example:

 ```yaml
string: "constant"        # still red
constant: "base05"        # more red
base05: "ff0000"          # red
name_variable: "ff0000"   # red
```

All the above resolve to red.

- `string` refers to `constant`
- `constant` refers to `base05`
- `base05` refers to the literal hex color red
- `name_variable` also refers to the literal hex color red

Note: The ordering does not matter, you can refer to an alias before that alias has been defined.


### Custom Slots

You may also define custom slots to make your scheme easier to author/maintain. For example if you hues are visually distinct it may be helpful to use custom slots to name them:

```yaml
scheme: "Fun Colors"
lightsaber_purple: "fe00ef"
granny_smith_red: "ee1122"
mr_blue_sky: "336699"
base0b: lightsaber_purple
base0c: granny_smith_red
base0d: mr_blue_sky
```

## Notes

### You are still limited to a max of 16 colors.

The number of colors per scheme is still limited to 16.  If you (via aliases) use more than 16 unique hex colors an error will be thrown during the build process.
