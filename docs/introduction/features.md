# Main features of Practicalli Neovim

A clean UI provides for a distraction free development experience, with only the essential information presented in the Neovim statusline or inline with the code

* [conjure] automatic Clojure REPL connection if nREPL process is running for a project
* [cmp & lsp] language auto-completion and snippet support
* [lsp] inline lint feedback whilst typing, references and unit test coverage
* [lualine] statusline with LSP status, diff changes, filetype, cursor position
* [telescope] completion of files, packages, colorschemes, etc
* [nvim-tree] visual file system navigation
* [gitsigns] gutter indicators for changed lines
* [todo comments] todo, fix, notes, indicators with gutter icons
* relative line numbers for vim-style navigation

<!-- TODO: add screenshots of features -->

## Conjure

An interactive environment for evaluating code, e.g. a Clojure REPL.  Conjure automatically connects to an nREPL process running in the current project.

Evaluate Clojure code as its developed for an instant feedback workflow.


## Language Server Protocol

nvim-treesitter provides a client for LSP servers, e.g. Clojure LSP.  Provides live linting feedback in the buffer browser and status line as well as language specific autocompletion

<!-- TODO: screenshot of LSP feedback, error popup and statusline indicators -->

## Telescope

Navigate files, packages and any other list of items effectively using Telescope.

<!-- TODO: screeshot of telescope file browser, project files and package list -->


## Git support

Octo provides a rich client, similar to Magit for Emacs.

<!-- TODO: screenshot of octo with staged and unstaged changes -->

Gitsigns hightlights buffer changes in the gutter

Lualine shows number of Git changes in status line

<!-- TODO: screenshot of buffer with added, changed and deleted changes, with indicators in status line -->

> Fugutive package is installed, although key bindings are not configured.  See `:help fugitive`


## File and directory navigation

nvim-tree provides a visual file system explorer that can also create and delete files and directories

Telescope File browser popup also explores the file system and in Normal mode can be used to create files and directories

<!-- TODO: screenshot of telescope file browser -->


## TODO Comments

Highlight tasks, fixes, notes and dragons comments, including icons in the gutter.  Use Telescope to navigate TODO comments in the current project.

<!-- TODO screenshot of several todo comment styles and telescope list of todo comments -->
