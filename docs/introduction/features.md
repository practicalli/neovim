# Common features in Practicalli Neovim

A clean UI provides for a distraction free development experience, with only the essential information presented in the Neovim statusline or inline with the code

* Plug-in Manager - Lazy or Packer
* [Clojure](#clojure) - automatic Clojure REPL connection, evaluation, test runners
* [LSP](#language-server-protocol) - auto-completion, snippets, inline linting, reference navigation, refactor and unit test coverage
* [statusline](#status-line) - LSP status, diff changes, filetype, cursor position
* [Selection narrowing](#selection-narrowing) completion of files, packages, color schemes, etc
* [Navigation](#navigation-and-selection-narrowing) - telescope selection narrowing and visual file system navigation
* [Version Control](#version-control) gutter indicators for changed lines
* [todo comments](#todo-comments) todo, fix, notes, indicators with gutter icons
* relative line numbers for vim-style navigation

??? WARNING "Work In Progress"


## Clojure

[:fontawesome-solid-book-open: Conjure](/neovim/repl-driven-development/conjure/) An interactive environment for evaluating code, e.g. a Clojure REPL.  Conjure automatically connects to an nREPL process running in the current project.

Evaluate Clojure code as its developed for an instant feedback workflow.

Run unit tests with Kaocha test runner (Cognitect Labs and ClojureScript runners also available)


## Language Server Protocol

Neovim includes an LSP client to present diagnostic information from LSP servers, e.g. Clojure LSP.  

LSP provides live linting feedback in the buffer browser and status line as well as language specific auto-completion

<!-- TODO: screenshot of LSP feedback, error popup and statusline indicators -->


## Selection Narrowing

Navigate files, packages, environment variables, ports, colour schemes (themes) and any other list of items effectively using Telescope.

Telescope File browser popup also explores the file system and in Normal mode can be used to create files and directories

The telescope list narrows matches as characters are typed

<!-- TODO: screeshot of telescope file browser, project files and package list -->


## Version Control

[Gitsigns](https://github.com/lewis6991/gitsigns.nvim) hightlights buffer changes in the gutter

Lualine shows number of Git changes in status line
<!-- TODO: screenshot of buffer with added, changed and deleted changes, with indicators in status line -->

[Diffview](https://github.com/sindrets/diffview.nvim) to review all changes for any git revision

[Neogit](https://github.com/TimUntersberger/neogit) provides a rich git client to add, stash, commit, push & pull changes.

[Octo](https://github.com/pwntester/octo.nvim) provides a GitHub specific client to manage issues and pull requests, using GitHub CLI authentication.

<!-- TODO: screenshot of octo with staged and unstaged changes -->

LazyGit UI


## Navigation

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
