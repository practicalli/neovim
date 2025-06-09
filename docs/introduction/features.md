# Neovim features

A clean UI provides for a distraction free development experience, with only the essential information presented in the Neovim statusline or inline with the code

!!! INFO "Neovim News for new developments"
    Keep up to date with new features within Neovim

    ```shell
    :help news
    ```

    View the news from a previous verion of Neovim
    ```shell
    :help news-0.10
    ```


## Clojure development

Support for the Clojure programming language, providing tools for REPL driven development.

- [Conjure REPL client](#conjure) - automatic Clojure REPL connection, evaluation, test runners
- [Clojure LSP](#language-server-protocol) - auto-completion, snippets, inline linting, reference navigation, refactor and unit test coverage
- Structural editing with paredit and parinfer
- Clojure snippets for common code and config
- Babashka files set to Clojure filetype (feedback welcome on Babashka support)
- JSON support


### Conjure

[:fontawesome-solid-book-open: Conjure](/neovim/repl-driven-development/conjure/) An interactive environment for evaluating code, e.g. a Clojure REPL.  Conjure automatically connects to an nREPL process running in the current project.

Evaluate Clojure code as its developed for an instant feedback workflow.

Run unit tests with Kaocha test runner (Cognitect Labs and ClojureScript runners also available)


## Plugin manager & Tools Manager

Lazy.nvim manages neovim plugins with a rich UI that provides an enjoyable user experience.  Plugins are automatically installed during startup and lists the status of each plugins.

Plugins are automatic cached & bytecode compiled and can be lazy loaded to streamline startup time and resource usage based on events, commands, filetypes, and key mappings.  Efficient plugin downloads using partial blob-less clones of plugin repositories, i.e. `--filter=blob:none`

![Lazy package manager UI](https://user-images.githubusercontent.com/292349/208301737-68fb279c-ba70-43ef-a369-8c3e8367d6b1.png){loading=lazy}

[:fontawesome-brands-github: Lazy.nvim](https://github.com/folke/lazy.nvim){target=_blank .md-button}

Mason installs and updates LSP servers, format and lint tools.


## Treesitter

Incremental parsing of code for efficient manipulation and decoration (syntax highlighting, errors, warnings, etc.)

Tree-sitter parses files opened in Neovim and builds a concrete syntax tree that any Neovim plugin can use to efficiently provide feedback. Treesitter uses incremental parsing to efficiently update the syntax tree as a file is edited.

- parse on every keystroke in a text editor
- provide useful results even in the presence of syntax errors

[:globe_with_meridians: Treesitter](https://tree-sitter.github.io/tree-sitter/){target=_blank .md-button}


## Language Server Protocol

Neovim includes an LSP client which uses the information recieved from a language specific LSP server in real-time to provide a range of services:

- auto-completion of function and symbol names
- live linting as code is typed or opened from a file
- formatting
- function signatures and help documentation
- diagnostics (syntax errors & idioms)
- symantic analysis providing rename through project, go-to-definition & find-references

LSP feedback is often presented in the buffer, file browser and status line of Neovim.

!!! INFO "LSP Server implementation is not universal"
    LSP is a relatively new specification and many server implmentations are still evolving or are yet to be created.

    Lint tools tend to be more prevelent and may be required in concert with or in the absence of an LSP server.

<!-- TODO: screenshot of LSP feedback, error popup and statusline indicators -->

??? INFO "LSP related Plugins"
    - neovim/nvim-lspconfig - connect Neovim lsp client to lsp servers
    - jose-elias-alvarez/null-ls.nvim - hook format and lint tools into the Neovim LSP client
    - jayp0521/mason-null-ls.nvim - automatically install formatters/linters to be used by null-ls
    - williamboman/mason - install and manage LSP servers, DAP servers, linters, and formatters
    - williamboman/mason-lspconfig - register LSP configs with neovim so LSP client can connect to  servers


## Lint and format tools:

Linters check code for common problems and provide hints on how to correct any detected issues.

Format tools suppor code to conforming to a specified coding style, typically these run when save-file is run.

null-ls provides extensive builtin configuration for programming languages and configuration formats.  null-ls also passes lint and format tool information to the Neovim LSP client, extending the range of language support.


## Selection Narrowing

[:fontawesome-brands-github: telescope.nvim](https://github.com/nvim-telescope/telescope.nvim){target=_blank} is a highly extendable fuzzy finder over lists with community driven pickers, sorters and previewers.

Navigate and narrow lists of files, packages, environment variables, ports, colour schemes (themes) and any other list of items effectively.

Telescope File browser popup also explores the file system and in Normal mode can be used to create files and directories

The telescope list narrows matches as characters are typed

<!-- TODO: screeshot of telescope file browser, project files and package list -->


## Version Control

- [Source code management](#version-control) gutter indicators for changed lines and staging changes from buffer

[Gitsigns](https://github.com/lewis6991/gitsigns.nvim) hightlights buffer changes in the gutter

[Diffview](https://github.com/sindrets/diffview.nvim) to review all changes for any git revision

[Neogit](https://github.com/TimUntersberger/neogit) provides a rich git client to add, stash, commit, push & pull changes (like Emacs Magit & VSCode Edamagit).

LazyGit integration (requires local lazygit install)

[Octo](https://github.com/pwntester/octo.nvim) provides a GitHub specific client to manage issues and pull requests, using GitHub CLI authentication.

<!-- TODO: screenshot of octo with staged and unstaged changes -->

LazyGit UI



## File Browser

neo-tree provides a visual file system explorer that can also create and delete files and directories


<!-- TODO: screenshot of telescope file browser -->


## TODO Comments

Highlight tasks, fixes, notes and dragons comments, including icons in the gutter.  Use Telescope to navigate TODO comments in the current project.

<!-- TODO: screenshot of several todo comment styles and telescope list of todo comments -->

## Status Line

LSP feedback


## Markdown

* LSP server
* Marksman: select anchors and pages for links


## General Editing tools

- [todo comments](#todo-comments) todo, fix, notes, indicators with gutter icons
- relative line numbers for vim-style navigation
- Clojure LSP server install & integration (install via mason or local install)
- Switch between associate src and test files (speeds up writing/fixing tests) :gratitude: to @dominicm
- Treesitter highlighting & rainbow delimiters
- Search & Replace (grug-far)
- Multiple Cursors

## UI

- [Selection narrowing (Snacks picker)](#selection-narrowing) completion of files, packages, colour schemes, etc
- Folke Snacks picker & Notifications
- Noice fancy command line UI
- [File browser](#file-browser) - selection narrowing and visual file system navigation
- [statusline](#status-line) - LSP status, diff changes, filetype, cursor position


## Colorschemes & Themes

Catppuccin is a very clean theme with Treesitter integration and support from a wide range of Neovim plugins.

Astro5 also includes a color selector and color code highlighting.

Emoji completions are shown when typing `:`

Neovide (GUI) integration (scaling fonts, etc)
Show key presses in when Neovim normal mode (demos, screen-casts)
