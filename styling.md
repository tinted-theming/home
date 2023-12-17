_The original version of this spec can be found at [chriskempson/base16](https://github.com/chriskempson/base16/blob/main/styling.md). The document is reproduced here for both convenience and archival purposes. We have made minor formatting changes to improve readability, content changes to reflect how these guidelines are applied in practice, and added an example._

---

# Base16 Styling Guidelines
**Version 0.3**

Base16 aims to group similar language constructs with a single color. For example, floats, ints, and doubles would belong to the same colour group. The colors for the default scheme were chosen to be easily separable, but scheme designers should pick whichever colours they desire, e.g. `base0B` (green by default) could be replaced with red. There are, however, some general guidelines below that stipulate which `base0B` should be used to highlight each construct when designing templates for editors.

Since describing syntax highlighting can be tricky, please see [base16-vim](https://github.com/tinted-theming/base16-vim/) and [base16-emacs](https://github.com/tinted-theming/base16-emacs/) for reference. Though it should be noted that each editor will have some discrepancies due the fact that editors generally have different syntax highlighting engines.

Colors `base00` to `base07` are typically variations of a shade and run from darkest to lightest. These colors are used for foreground and background, status bars, line highlighting and such. Colors `base08` to `base0F` are typically individual colors used for types, operators, names and variables. In order to create a dark scheme, colors base00 to `base07` should span from dark to light. For a light scheme, these colours should span from light to dark.

- **base00** - Default Background
- **base01** - Lighter Background (Used for status bars, line number and folding marks)
- **base02** - Selection Background
- **base03** - Comments, Invisibles, Line Highlighting
- **base04** - Dark Foreground (Used for status bars)
- **base05** - Default Foreground, Caret, Delimiters, Operators
- **base06** - Light Foreground (Not often used)
- **base07** - Brightest Foreground (Not often used)
- **base08** - Variables, XML Tags, Markup Link Text, Markup Lists, Diff Deleted
- **base09** - Integers, Boolean, Constants, XML Attributes, Markup Link Url
- **base0A** - Classes, Markup Bold, Search Text Background
- **base0B** - Strings, Inherited Class, Markup Code, Diff Inserted
- **base0C** - Support, Regular Expressions, Escape Characters, Markup Quotes
- **base0D** - Functions, Methods, Attribute IDs, Headings
- **base0E** - Keywords, Storage, Selector, Markup Italic, Diff Changed
- **base0F** - Deprecated, Opening/Closing Embedded Language Tags, e.g. `<?php ?>`

_SPEC END_

---

Here is an example of a typical Base16 scheme:

**ashes.yaml**

```yaml
scheme: "Ashes"
author: "Jannik Siebert (https://github.com/janniks)"
base00: "1C2023" # ---- dark
base01: "393F45" # ---
base02: "565E65" # --
base03: "747C84" # -
base04: "ADB3BA" # +
base05: "C7CCD1" # ++
base06: "DFE2E5" # +++
base07: "F3F4F5" # ++++ light
base08: "C7AE95" # orange
base09: "C7C795" # yellow
base0A: "AEC795" # poison green
base0B: "95C7AE" # turquois
base0C: "95AEC7" # aqua
base0D: "AE95C7" # purple
base0E: "C795AE" # pink
base0F: "C79595" # light red
```
