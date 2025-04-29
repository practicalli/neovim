# Refactor tools

Neovim and common plugins provide many text oriented tools useful for refactoring code.

Clojure LSP server and Neovim LSP client support use static analysis of the project source code to allow provide common code refactor tools.

## Language Server Protocol (LSP)

Using [clojure-lsp](https://clojure-lsp.io/) server and [Neovim Treesitter](https://tree-sitter.github.io/tree-sitter/) as an LSP client, code is statically analysed to provide auto-completion data, advanced editing actions such as refactor, live formatting, etc.

### Function documentation

++"K"++ or ++spc++ ++"l"++ ++"h"++ show the doc-string for function or any other var under the cursor.

Repeat the key binding to move the cursor to the documentation popup window and use ++"j"++ ++"k"++ to scroll the documentation

++comma++ ++"l"++ ++"l"++ code lens refresh

++comma++ ++"l"++ ++"L"++ code lens run


### Navigation

++"g"++ ++"d"++ go to definition of current symbol, e.g. function definition

++comma++ ++"l"++ ++"G"++ telescope search of all symbols in the project

++comma++ ++"l"++ ++"R"++ telescope search of all references in the project

++comma++ ++"l"++ ++"s"++ telescope search of symbols

++comma++ ++"l"++ ++"s"++ split view of symbols


### Diagnostics

++spc++ ++"l"++ ++"d"++ show popup for current diagnostic indicator

++spc++ ++"l"++ ++"D"++ search through all diagnostics reports


### Code Actions

++spc++ ++"l"++ ++"r"++ rename current symbol (namespace rename not supported by Neovim LSP client)

++spc++ ++"l"++ ++"a"++ code actions (popup with available actions)

++spc++ ++"l"++ ++"f"++ format buffer


### Rename namespace

Clojure LSP can rename namespaces and update the corresponding file name.

The Neovim LSP client does not seem to support file renaming so the ++spc++ ++"l"++ ++"r"++ command fails.

Clojure LSP can be called via the command line to rename the namespace and its corresponding file name.

!!! NOTE "Rename namespace via Clojure LSP on Command Line"
    ```shell
    clojure-lsp rename --from gameboard.gameboard.api.scoreboard --to practicalli.gameboard.api.scores
    ```

> [nvim-lsp-file-operations](https://github.com/antosha417/nvim-lsp-file-operations) was tried but without success so far.


<!--
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

-->

### Troubleshooting

++spc++ ++"l"++ ++"i"++ shows the LSP server information for the current filetype, e.g. Clojure

![LSP Server information showing local clojure-lsp install](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lsp-clojure-server-information-local-install-light.png?raw=true#only-light){loading=lazy}
![LSP Server information showing local clojure-lsp install](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lsp-clojure-server-information-local-install-dark.png?raw=true#only-dark){loading=lazy}

++spc++ ++"l"++ ++"I"++ shows format and lint tools supported by null-ls for the current filetype, e.g. clojure


## Limitations to investigate

* Neovim client does not seem to support namespace rename (AstroNvim)
