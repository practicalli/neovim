# Snippets

[LuaSnip](https://github.com/L3MON4D3/LuaSnip) can use several different sources for snippets

- VSCode JSON snippets ([Friendly-snippets](https://github.com/rafamadriz/friendly-snippets/tree/main/snippets))
- [LSP style snippets](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#snippet_syntax) 

??? EXAMPLE "LuaSnip Configuration"
    [Practicalli Neovim Config Redux](https://github.com/practicalli/neovim-config-redux) includes the LuaSnip package which also adds friendly-snippets and cmp_luasnip.
    ```fennel
      ; snippets
      :L3MON4D3/LuaSnip 
      {:requires [:rafamadriz/friendly-snippets
                  :saadparwaiz1/cmp_luasnip]
       :mod :lua-snip}
    ```
    Configure LSP snippet locations
    ```json
    {
      "name": "practicalli-snippets",
      "engines": {
        "vscode": "^1.11.0"
      },
      "contributes": {
        "snippets": [
          {
            "language": [
              "markdown",
              "global",
              "all"
            ],
            "comment": "snippets accross several languages",
            "path": "./global.json"
          },
          {
            "language": 
              "markdown",
            "path": "./markdown.json"
          }
        ]
      }
    }
    ```

## Snippet Definitions

`snippets` directory contains snippet definitions, with a JSON file for each language, e.g. `markdown.json`

[Practicalli Neovim Config Redux](https://github.com/practicalli/neovim-config-redux) contains several groups of snippet definitions

- MkDocs format and icons (`markdown.json` VSCode syntax)

!!! HINT "Restart Neovim to load new defintions"
    Snippets added to VSCode JSON snippets are only loaded when Neovim starts, so newly added snippets will only be available after Neovim is restarted.

