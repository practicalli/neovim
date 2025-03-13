# Refactor

Neovim has several built-in tools for general refactor and debugging.

Most languages are suppored by an LSP server which provides common refactor tools across editors (when the server is fully implemented).


## Language Server Protocol

Neovim provides a Language Server Protocol (LSP) client that uses a language specific LSP server to provides code refactoring features using semantic analysis of the current project.

- find-references
- rename
- code actions (convert to function, let, etc)


# Search and Replace in Multiple Buffers

There are multiple ways to search and replace a pattern in multiple buffers. We can use the commands listed below to search and replace a pattern in multiple buffers.

- `:argdo` — command for each file in the argument list
- `:bufdo` — command in each buffer in the buffer list
- `:tabdo` — command in each tab page
- `:windo` — command in each window
- `:cdo` — entry in the quickfix list
- `:cfdo` — file in the quickfix list


## Quickfix

Quickfix mode is used to speedup the edit-compile-edit cycle by saving error messages in a file that is then used to jump to relevant places in the code base.

This allow addressing all of the errors generated without having to remember each and every error.

Any generated list of position in a file can be used by Quickfix for more general editing speedups.

> NOTE: Commonly used quickfix commands: `:cclose`, `:cnext`, `:copen`, `:grep`, `:make`

Quickfix commands to try:

- `:copen` opens the quickfix window
- `:cclose` or `:ccl` closes quickfix window
- `:cw` open it if there are "errors", close it otherwise
- `:cn` Go to the next error in the window
- `:cp` Go to the previous error in the window
- `:cnf` Go to the first error in the next file
- `:.cc`  Go to error under cursor (if cursor is in quickfix window)


[Quickfix - Neovim docs](https://neovim.io/doc/user/quickfix.html){target=_blank .md-button}
