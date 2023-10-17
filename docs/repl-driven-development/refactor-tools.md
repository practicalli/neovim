# Refactor tools

Neovim and common plugins provide many text oriented tools useful for refactoring code.

Clojure LSP server and Neovim LSP client support use static analysis of the project source code to allow provide common code refactor tools.

## Language Server Protocol (LSP)

Using [clojure-lsp](https://clojure-lsp.io/) server and [Neovim Treesitter](https://tree-sitter.github.io/tree-sitter/) as an LSP client, code is statically analysed to provide auto-completion data, advanced editing actions such as refactor, live formatting, etc.

!!! HINT "Function help"
    `SPC l h` or ++"K"++ displays help for the function under the cursor

    Repeat the key binding to move the cursor to the documentation popup window and use ++"j"++ ++"k"++ to scroll the documentation


### Key maps

=== "Practicalli AstroNvim Config"

    - `<leader>la` code actions (popup with available actions)
    - `<leader>ld` hover diagnostics
    - `<leader>lD` search diagnostics
    - `<leader>lf` format buffer
    - `<leader>lG` search workspace symbols
    - `<leader>lh` function signature help
    - `<leader>li` information about the LSP client and running LSP servers
    - `<leader>lI` null-ls information (format & lint tools)
    - `<leader>ll` code lens refresh
    - `<leader>lL` code lens run
    - `<leader>lr` rename current symbol (namespace rename not supported it seems)
    - `<leader>lR` search references
    - `<leader>ls` search symbols
    - `<leader>lS` symbols outline

=== "Practicalli Neovim Config Redux"

    - `gd` Go to definition
    - `K` Show documentations
    - `<leader>ld` Function declarations
    - `<leader>lt` Type Definitions
    - `<leader>lh` Signature Help
    - `<leader>ln` Rename
    - `<leader>le` Show line diagnostics
    - `<leader>lq` Show all diagnostics information
    - `<leader>lf` Auto format
    - `<leader>lj` Go to next diagnostic
    - `<leader>lk` Go to previous diagnostic
    - `<leader>la` Open code actions menu (Using telescope plugin interface)
    - `<leader>la` Open code actions menu for the selected text in **VISUAL mode** (Using telescope plugin interface)
    - `<leader>lw` Open workspace diagnostics list (Using telescope plugin interface)
    - `<leader>lr` Show all references list for item under the cursor (Using telescope plugin interface)
    - `<leader>lr` Show all implementations list for item under the cursor (Using telescope plugin interface)


### Limitations to investigate

* Neovim client does not seem to support namespace rename (AstroNvim)
