# Structural Editing

Structural editing seeks to ensure that parenthesis (parens) and other pairs of characters remain balanced, i.e. an open paren is not removed without removing the closing paren.

- parinfer uses an indent approach, aligning code manages parens locations
- paredit uses a structural approach


??? INFO "AstroNvim Community Clojure Pack includes parinfer"
    [nvim-parinfer](https://github.com/gpanders/nvim-parinfer) plugin is included in the [AstroNvim Community Clojure pack](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/pack/clojure)
    
    ```lua
      { import = "astrocommunity.pack.clojure" },
    ```
## Parinfer
Parinfer works very well with vim-style modal editing.

The author of the code focuses on aligning code and parinfer takes care of balancing the parens.

To include new lines of code within an expression, create a new line `o` and indent.

Parinfer will move the preceeding closing paren(s) to the new line, enclosing the new code in the overall expression.

[Parinfer website](https://shaunlebron.github.io/parinfer/){target=_blank .md-button} 
