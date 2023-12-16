# Changelog

## 0.11.0 (Dec 15, 2023)

- Create a new "common scheme format" with the following changes from the legacy base16 format:
  - Add `system` to scheme files
  - Add `slug` to scheme files, replacing using the filename as the slug
  - Add `variant` to scheme files
- Add the following template variables:
  - Add `scheme-variant` as a template variable
  - Add `scheme-slug-underscored` as a template variable
  - Add `scheme-is-{{ variant }}-variant` as a template variable
- Add `filename` to the template config
- Add `supported-systems` to template config
- Specify that the `slug` should be calculated from the `name` rather than the filename when missing
- Add specific definition of our slugify method which works with Unicode
- Add information about the structure of the new [schemes repository](https://github.com/tinted-theming/schemes)

All of these have the following impact:

- Changes to scheme files can now be made without breaking old builders
- New common scheme files are self-contained - the filename no longer matters
- Additional palette-based systems can be added without changes to the spec

## 0.10.0 (Mar 20, 2021)

- Simplify repo structure and builder responsibilities
- Clarify that using a hash as a part of the color is allowed

## 0.9.1 (Jun 15, 2019)

- Make baseXX-hex-bgr variables available to templates
- Warn when a template file has been overwritten

## 0.9.0 (Jul 6, 2017)

- Add decimal color variables

## 0.8.1 (Dec 29, 2016)

- Clarify theme filename generation
- Various clarifications

## 0.8.0 (Aug 27, 2016)

- Drop support for HSL variables
