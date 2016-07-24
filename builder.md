# Builder Guidelines
**Version 0.7**

A base16 builder is an application that can build sytax highligting definition files for text editors by using base16 scheme files which contain a collection of colours and base16 template files which contain synax highlighting rules. A builder uses Git as the mechanism to download and keep uptodate sytax files and template files.

## File Structure
- `/` - Contains anything you consider appropriate for your builder
- `/sources.yaml` - Holds a list of source respositories for schemes and templates
- `/sources/schemes/list.yaml` - Holds a list of scheme respositories
- `/sources/templates/list.yaml` - Holds a list of template respositories
- `/schemes/[name]/*.yaml` - A scheme file (there may be multiples of these)
- `/templates/[name]/templates/*.mustache` - A template file (there may be multiples of these)
- `/templates/[name]/templates/config.yaml` - A template configuration file

## Workflow
The first job a just-installed builder has is to populate a list of scheme sources and template sources. It does this by parsing the `/sources.yaml` file and using git to download the defined repositories to `/sources`. Next a builder will parse the downloaded `/sources/schemes/list.yaml` and download the defined repositories to `/schemes`. Finally a builder will parse the downloaded `/sources/templates/list.yaml` and download the defined repositories to `/templates`. All this is performed by the `builder update` command which can also be used to update sources, schemes and teamplates.

When building themes by running `builder`, a base16 builder should first clear out any old output then iterate through all the scheme files in `/schemes` and for each scheme should iterate through all the template files in `/templates` producing themes that will be output to the template directories specified in `/templates/template_name/template/config.yaml`. The theme filename should look like `base16-[slug][extension]`. Where slug is taken from the scheme file and template_directory and extention is taken from `/template/config.yaml`.

## Template Variables
A builder should provide the following variables to a template file:

- `scheme-name` - obtained from the scheme file
- `scheme-author` - obtained from the scheme file
- `scheme-slug` - obtained from the scheme file
- `base00-hex` to `base0F-hex` - obtained from the scheme file e.g "7cafc2"
- `base00-hex-r` to `base0F-hex-r` - built from the hex value in the scheme file e.g "7c"
- `base00-hex-g` to `base0F-hex-g` - built from the hex value in the scheme file e.g "af"
- `base00-hex-b` to `base0F-hex-b` - built from the hex value in the scheme file e.g "c2"
- `base00-rgb-r` to `base0F-rgb-r` - converted from the hex value in the scheme file e.g "124"
- `base00-rgb-g` to `base0F-rgb-g` - converted from the hex value in the scheme file e.g "175"
- `base00-rgb-b` to `base0F-rgb-b` - converted from the hex value in the scheme file e.g "194"
- `base00-hsl-h` to `base0F-hsl-h` - converted from the hex value in the scheme file e.g "196"
- `base00-hsl-s` to `base0F-hsl-s` - converted from the hex value in the scheme file e.g "36"
- `base00-hsl-l` to `base0F-hsl-l` - converted from the hex value in the scheme file e.g "62"

## Code Structure
There is no outline for a recommended code structure that a base16 theme builder should follow but a design goal should be to keep the application as simple as possible providing only the functionality desibed in this document. If you feel you have a great idea for additional functionality please raise an issue in the [base16 repository](https://github.com/chriskempson/base16).

## Considerations
Mustache was chosen as the templating language due to its simplicity and widespread adoption across languages. Yaml was chosen to describe scheme and configuration files for the same reasons.
