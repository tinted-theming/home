_The original version of this spec can be found at [chriskempson/base16](https://github.com/chriskempson/base16/blob/main/styling.md). The document is reproduced here for both convenience and archival purposes. We have made minor formatting changes to improve readability, content changes to reflect how these guidelines are applied in practice, and added an example._

---

# Base16 Styling Guidelines
**Version 0.4.2**

Base16 aims to group similar language constructs with a single color. For example, floats, ints, and doubles would belong to the same colour group. The colors for the default scheme were chosen to be easily separable, but scheme designers should pick whichever colours they desire, e.g. `base0B` (green by default) could be replaced with red. There are, however, some general guidelines below that stipulate which `base0B` should be used to highlight each construct when designing templates for editors.

Since describing syntax highlighting can be tricky, please see [base16-vim](https://github.com/tinted-theming/base16-vim/) and [base16-emacs](https://github.com/tinted-theming/base16-emacs/) for reference. Though it should be noted that each editor will have some discrepancies due the fact that editors generally have different syntax highlighting engines.

Colors `base00` to `base07` are typically variations of a shade and run from darkest to lightest for dark themes. These colors are used for foreground and background, status bars, line highlighting and such. Colors `base08` to `base0F` are typically individual colors used for types, operators, names and variables. In order to create a dark scheme, colors `base00` to `base07` should span from dark to light. For a light scheme, these colours should span from light to dark.

## Usage Guidelines

We offer guidelines for both dark and light themes:

### Dark

- Colours from `base00` to `base07` should range from dark to light.

### Light

- Colours from `base00` to `base07` should range from light to dark.

## Specific Colours and Their Usages

  Each colour (base0X) serves a specific purpose or use case, such as background, foreground, variables, errors, etc. Here's a breakdown using the "One Dark" scheme colors:

| Color                                              | base0X | Ansi     | Terminal                 | Text Editor |
| -------------------------------------------------- | ------ | -------- | ------------------------ | ----------- |
| ![#](https://placehold.it/25/282c34/000000?text=+) | base00 | -        | Background               | Default Background |
| ![#](https://placehold.it/25/3f4451/000000?text=+) | base01 | 0        | Black                    | Lighter Background (Used for status bars) |
| ![#](https://placehold.it/25/4f5666/000000?text=+) | base02 | 8        | Bright Black             | Selection Background |
| ![#](https://placehold.it/25/545862/000000?text=+) | base03 | -        | (Gray)                   | Comments, Invisibles, Line Highlighting |
| ![#](https://placehold.it/25/9196a1/000000?text=+) | base04 | -        | (Light Gray)             | Dark Foreground (Used for status bars) |
| ![#](https://placehold.it/25/abb2bf/000000?text=+) | base05 | -        | Foreground               | Default Foreground, Caret, Delimiters, Operators |
| ![#](https://placehold.it/25/e6e6e6/000000?text=+) | base06 | 7        | White                    | Light Foreground |
| ![#](https://placehold.it/25/ffffff/000000?text=+) | base07 | 15       | Bright White             | The Lightest Foreground |
| ![#](https://placehold.it/25/e06c75/000000?text=+) | base08 | 9  and 1 | Bright Red and Red       | Variables, XML Tags, Markup Link Text, Markup Lists, Diff Deleted |
| ![#](https://placehold.it/25/d19a66/000000?text=+) | base09 | ~3       | (Orange)                 | Integers, Boolean, Constants, XML Attributes, Markup Link Url |
| ![#](https://placehold.it/25/e5c07b/000000?text=+) | base0A | 11 and 3 | Bright Yellow and Yellow | Classes, Markup Bold, Search Text Background |
| ![#](https://placehold.it/25/98c379/000000?text=+) | base0B | 10 and 2 | Bright Green and Green   | Strings, Inherited Class, Markup Code, Diff Inserted |
| ![#](https://placehold.it/25/56b6c2/000000?text=+) | base0C | 14 and 6 | Bright Cyan and Cyan     | Support, Regular Expressions, Escape Characters, Markup Quotes |
| ![#](https://placehold.it/25/61afef/000000?text=+) | base0D | 12 and 4 | Bright Blue and Blue     | Functions, Methods, Attribute IDs, Headings |
| ![#](https://placehold.it/25/c678dd/000000?text=+) | base0E | 13 and 5 | Bright Purple and Purple | Keywords, Storage, Selector, Markup Italic, Diff Changed |
| ![#](https://placehold.it/25/be5046/000000?text=+) | base0F | -        | (Dark Red or Brown)      | Deprecated, Opening/Closing Embedded Language Tags, e.g. `<?php ?>` |

**Notes**:

- These are just guidelines and will most often provide best results when the they are followed.
- Items in parenthesis in the Terminal column do not have an identified terminal use and are a more generic colour description.

## YAML scheme example

**ayu-dark.yaml**

```yaml
system: "base16"
name: "Ayu Dark"
author: "Khue Nguyen <Z5483Y@gmail.com>"
variant: "dark"
palette:
  base00: "0f1419" # ---- dark
  base01: "131721" # ---
  base02: "272d38" # --
  base03: "3e4b59" # -
  base04: "bfbdb6" # +
  base05: "e6e1cf" # ++
  base06: "e6e1cf" # +++
  base07: "f3f4f5" # ++++ light
  base08: "f07178" # red
  base09: "ff8f40" # orange
  base0A: "ffb454" # yellow
  base0B: "b8cc52" # green
  base0C: "95e6cb" # cyan
  base0D: "59c2ff" # blue
  base0E: "d2a6ff" # purple
  base0F: "e6b673" # brown
```

_SPEC END_

---
