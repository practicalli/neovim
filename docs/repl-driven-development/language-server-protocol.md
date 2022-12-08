# Language Server Protocol (LSP) Configuration

Using [clojure-lsp](https://clojure-lsp.io/) server and [Neovim Treesitter](https://tree-sitter.github.io/tree-sitter/) as an LSP client, code is statically analysed to provide auto-completion data, advanced editing actions such as refactor, live formatting, etc.

## Key maps


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
