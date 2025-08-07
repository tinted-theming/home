# ANSI8 Styling Guidelines

**Version 0.1.0** The latest version of this spec can be obtained from
[tinted-theming/specs/ansi8/styling](https://github.com/tinted-theming/home/blob/main/specs/ansi8/styling.md)

ANSI8 aims to make it very simple to style terminal based applications, but can
be heavily expanded to style complex GUI applications. ANSI8 simplifies the
process of creating a color scheme by asking the user to only specify the 8
basic ANSI colors. The builder will then generate all additional colors,
including bright variants, "Black" to "White" gradients, and dim variants.

In this model, the core 8 ANSI colors represent a palette, and the builder
handles the generation of other necessary colors. The design follows a basic
rule where:

- `ansi0` to `ansi7` are the primary 8 ANSI colors (user-defined).
- Bright variants and dim variants of these 8 colors are automatically
  generated.
- Grayscale gradients from "Black" to "White" are calculated based on `ansi0`
  and `ansi7` for smooth transitions.
- Gradient generation starts from `ansi0` ("Black") to `ansi7` ("White"), and this
  gradient is used in various areas like backgrounds, text, and status bars.


## Usage Guidelines

We offer guidelines for both dark and light themes:

### Dark

- `ansi0` should be dark and `ansi7` should be light.

### Light

- `ansi7` should be light and `ansi0` should be dark.

## Provided colors

| Color Name                                                             | ANSI Color | Description                           |
| ---------------------------------------------------------------------- | ---------- | ------------------------------------- |
| palette.black (![#](https://placehold.co/25/282c34/000000?text=%2B))   | 0          | Default background color (dark theme) |
| palette.red (![#](https://placehold.co/25/e06c75/000000?text=%2B))     | 1          | error messages                        |
| palette.green (![#](https://placehold.co/25/98c379/000000?text=%2B))   | 2          | Used for strings, success messages    |
| palette.yellow (![#](https://placehold.co/25/e5c07b/000000?text=%2B))  | 3          | Used for constants, warnings          |
| palette.blue (![#](https://placehold.co/25/61afef/000000?text=%2B))    | 4          | Used for functions, method names      |
| palette.magenta (![#](https://placehold.co/25/c678dd/000000?text=%2B)) | 5          | Used for keywords, selectors          |
| paletta.cyan (![#](https://placehold.co/25/56b6c2/000000?text=%2B))    | 6          | Used for support, regex patterns      |
| palette.white (![#](https://placehold.co/25/be5046/000000?text=%2B))   | 7          | Used for text and light backgrounds   |

These 8 colors will be used as the foundation. The builder will automatically
generate:

- **Standard variants**: These map to the provided values in the `.toml` file.
- **Bright variants**: These are brightened versions of each standard color.
- **Dim variants**: These are darker versions of each standard color.
- **Gray color**: A gray is generated from the midpoint of the `palette.black`
  and `palette.white` color. This is considered the "Standard" variant and will
  have Bright and Dim variants too.

## Generated colors

| Color Name      | ANSI Color | Description                           |
| --------------- | ---------- | ------------------------------------- |
| black_dim       | 0          | Default background color (dark theme) |
| black_default   | 0          | Default background color (dark theme) |
| black_bright    | 0          | Default background color (dark theme) |
| red_dim         | 1          | error messages                        |
| red_default     | 1          | error messages                        |
| red_bright      | 1          | error messages                        |
| green_dim       | 2          | Used for strings, success messages    |
| green_default   | 2          | Used for strings, success messages    |
| green_bright    | 2          | Used for strings, success messages    |
| yellow_dim      | 3          | Used for constants, warnings          |
| yellow_default  | 3          | Used for constants, warnings          |
| yellow_bright   | 3          | Used for constants, warnings          |
| blue_dim        | 4          | Used for functions, method names      |
| blue_default    | 4          | Used for functions, method names      |
| blue_bright     | 4          | Used for functions, method names      |
| magenta_dim     | 5          | Used for keywords, selectors          |
| magenta_default | 5          | Used for keywords, selectors          |
| magenta_bright  | 5          | Used for keywords, selectors          |
| cyan_dim        | 6          | Used for support, regex patterns      |
| cyan_default    | 6          | Used for support, regex patterns      |
| cyan_bright     | 6          | Used for support, regex patterns      |
| white_dim       | 7          | Used for text and light backgrounds   |
| white_default   | 7          | Used for text and light backgrounds   |
| white_bright    | 7          | Used for text and light backgrounds   |
| gray_dim        | 7          | Used for text and light backgrounds   |
| gray_default    | 7          | Used for text and light backgrounds   |
| gray_bright     | 7          | Used for text and light backgrounds   |

Sample YAML Scheme
Here’s how the ANSI8 specification would look in YAML format:

```toml
system = "ansi8"
name = "Ayu"
author = "User <user@example.com>"
variant = "dark"

[palette]
black   = "#131721"  # Black
red     = "#f07178"  # Red
green   = "#b8cc52"  # Green
yellow  = "#ffb454"  # Yellow
blue    = "#59c2ff"  # Blue
magenta = "#d2a6ff"  # Magenta
cyan    = "#95e6cb"  # Cyan
white   = "#e6e1cf"  # White
```

**Dev Notes**: Thoughts here could be to give the builder access to a dark and
light variant of a theme to allow it to solve things like this:
https://github.com/tinted-theming/tinted-terminal/issues/14

_SPEC END_

---
