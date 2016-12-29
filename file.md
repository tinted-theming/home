# File Guidelines
Base16 specifies the format of two types of files. Scheme files, used for defining the colors that are to be assigned to a template when processed by a Builder and Config files used by templates to pass information to a Builder when using a template.

## Template Config Files
    default: 
        extension: .file-extension
        output: output-directory-name

## Scheme Files
Scheme files have the following example structure:

    scheme: "Scheme Name"
    author: "Scheme Author"
    base00: "000000"
    base01: "111111"
    base02: "222222"
    base03: "333333"
    base04: "444444"
    base05: "555555"
    base06: "666666"
    base07: "777777"
    base08: "888888"
    base09: "999999"
    base0A: "aaaaaa"
    base0B: "bbbbbb"
    base0C: "cccccc"
    base0D: "dddddd"
    base0E: "eeeeee"
    base0F: "ffffff"
