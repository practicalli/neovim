# Changelog

## Unreleased
### Added
- nodejs requirement for mason lsp server install
- repl: initial page on structured editing with parinfer
- basic: Astronvim notification page with history navigation
- basics: configure neotree to show hidden files and directories
- install: add MacOSX homebrew section
- install: neovide install and configuration, Linux & MacOSX
- source-control: add nvimdiff configuration and use for Git diff views
- install: neovim GitHub release install on MacOSX
- basics: neovim registers guide
- basics: creating a directory with telescope or commands
- intro: add :help news to features page
 
### Changed
- ci: spell lychee & repository trufflehog linters warn only (false positives)
- intro: update fennel with nfnl project, replacing aniseed
- repl: refactor lsp page to refactor tools page
- repl: simplify conjure page and add more examples
- repl: update repl and external testing
- repl: update correct key bindings to open vertical and horizontal repl log split
- mkdocs: update material emoji extension name to support Material 9.4 (latest version)
- source-control: move version-control to source-control for consistency in Practicalli books
- intro: update sponsorship link and text in intro and readme
- intro: update pull request description
- basics: file marks for jumping within a file
- dev: add checklist and description sections to pull request template
- basics: navigate cursor location history


## 2023-07-11

### Added
- basics: vim-style search and replace
- basics: multiple cursors search and replace
- basics: astronvim multiple cursor use
- versioning: staging hunks and buffers with Git Signs
- apis: inspect JSON and call APIs from neovim
- basics: open web links

### Changed

- config: override clojure pack as hint
- config: extend user design overview
- config: user config overview
- config: override community key bindings


## 2023-05-14

### Added

- overrides for 404 page and announcement of neovim as alpha stage book

### Changed

- [#29](https://github.com/practicalli/neovim/issues/29) convert Neovim book to MkDocs version 9
- reference: start lua-language section, add references
- mkdocs: update Practicalli logo
- intro: standard book contributing, repl-workflow, writing-tips
- mkdocs: enable code blocks to embed content from files
- dev: update local mkdocs workflow in readme
- dev: update lint tasks for MkDocs
- dev: git ignore patterns for mkdocs
- ci: monthly version check via antq
