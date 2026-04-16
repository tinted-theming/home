# Contributing to Template Repositories

Tinted Theming template repository includes a [GitHub Action] that
builds the colorschemes once a week. This keeps the template up-to-date
with the [tinted-schemes] repository automatically.

## Building

[tinted-builder-rust] is recommended to build template repositories.
It's not required to be in any specific directory when building a
template because the `build` subcommand accepts absolute or relative
paths as arguments. To build the current working directory
`tinted-builder-rust build .` can be run.

### Dependencies

The following is the dependency list for building themes of a
tinted-theming template repository:

- [tinted-builder-rust] `>=0.11.0` 
- [git] `*` (any version)

### Usage for template editing

1. Install [tinted-builder-rust]
1. `tinted-builder-rust build path/to/your/tinted-template-repository`

Note: `path/to/your/tinted-template-repository` is a placeholder path
and should reflect the absolute or relative path to your local template
repository you want to build.

### Usage for adding or editing a colorscheme

1. Clone the tinted-template-repository locally, eg: [tinted-tmux]
1. Clone [tinted-schemes] locally
1. Install [tinted-builder-rust]
1. Execute:

   ```sh
   tinted-builder-rust build /path/to/tinted-tmux --schemes-dir /path/to/tinted-schemes
   ```

   Note: `path/to/tinted-tmux` and `path/to/tinted-schemes` are
   placeholders and should reflect the absolute or relative paths to
   your local template and schemes repositories.

#### Command Breakdown

A basic breakdown of the command used in the execute step above:

1. `tinted-builder-rust` - The CLI tool [tinted-builder-rust]
1. `build` - The `build` subcommand. This accepts 1 absolute or relative
   path to template repository argument.
1. `/path/to/tinted-template-repository` - The argument that the `build`
   subcommand accepts. This is the absolute or relative path to the
   template repository to build or generate themes for.
1. `--schemes-dir` - A CLI flag which specifies that a custom schemes
   repository should be used instead of cloning and using the latest
   [tinted-schemes] repository.
1. `/path/to/your/schemes-repo` - The path value associated with the
   `--schemes-dir` CLI flag.

Run `tinted-builder-rust --help` to explore more options and
subcommands. For more details refer to [tinted-builder-rust] README.md,
or open an [issue] on GitHub.

[Install tinted-builder-rust]: https://github.com/tinted-theming/tinted-builder-rust?tab=readme-ov-file#installation
[git]: https://git-scm.com/
[tinted-tmux]: https://github.com/tinted-theming/tinted-tmux
[tinted-schemes]: https://github.com/tinted-theming/schemes
[tinted-builder-rust]: https://github.com/tinted-theming/tinted-builder-rust
[GitHub Action]: .github/workflows/update.yml
[issue]: https://github.com/tinted-theming/tinted-builder-rust/issues
