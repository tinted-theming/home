# Builder Guidelines
A base16 builder is an application that can build sytax highligting definition files for text editors by using base16 scheme files which contain a collection of colours and base16 template files which contain synax highlighting rules. A builder uses Git as the mechanism to download and keep uptodate sytax files and template files.

## File Structure
- `schemes.yaml` - Holds a list of scheme respositories
- `templates.yaml` - Holds a list of template respositories
- `/schemes/scheme_name/scheme-dark.yaml` - A dark scheme file (optional if scheme is dark only)
- `/schemes/scheme_name/scheme-light.yaml` - A light scheme file (optional if scheme is light only)
- `/templates/editor_name/template.mustache` - A template file
- `/templates/editor_name/template-config.yaml` - template configuration file

## Workflow
When building themes a base16 builder should iterate through all the scheme files in `schemes` and for each scheme should iterate through all the template files in `templates`. 

## Variables
A builder should provide the following variables to a template file:

- `scheme-name` - obtained from the scheme file
- `scheme-author` - obtained from the scheme file
- `scheme-slug` - obtained from the scheme file
- `base00-hex` to `base0F-hex` - obtained from the scheme file
- `base00-hex-r` to `base0F-hex-r` - built from the hex value in the scheme file
- `base00-hex-g` to `base0F-hex-g` - built from the hex value in the scheme file
- `base00-hex-b` to `base0F-hex-b` - built from the hex value in the scheme file
- `base00-rgb-r` to `base0F-rgb-r` - converted from the hex value in the scheme file
- `base00-rgb-g` to `base0F-rgb-g` - converted from the hex value in the scheme file
- `base00-rgb-b` to `base0F-rgb-b` - converted from the hex value in the scheme file

## Operation
Running `base16` with no arguments should build all present scheme files and temlpate files. Running `base16 update` should update all scheme and template repositories.

## Architecture
There is no outline for the architecture that a base16 theme builder should follow but a design goal should be to keep the application as simple as possible providing only the functionality desibed in this document.

## Considerations
Mustache was chosen as the templating language due to its simplicity and widespread support across languages. Yaml was chosen to describe scheme and configuration files for the same reasons.
