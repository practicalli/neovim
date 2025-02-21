# Structural Editing

Structural editing ensures parenthesis (parens) and other pairs of characters remain balanced when entering or changing code, i.e. an open paren is not removed without removing the closing paren.

Parinfer and Paredit plugins provides a way to manage parens effectively

- [nvim-parinfer](https://github.com/gpanders/nvim-parinfer) manages the surrounding parens with indentation used for nested parens stuctures.
- [nvim-treesitter-sexp](https://github.com/PaterJason/nvim-treesitter-sexp) paredit features, automatic balancing of parens and commands to refactor code structure

!!! TIP "Practicalli recommends Parinfer & vim-style editing"

??? INFO "AstroNvim Community Clojure Pack includes parinfer & paredit"
    [nvim-parinfer](https://github.com/gpanders/nvim-parinfer) plugin is included in the [AstroNvim Community Clojure pack](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/pack/clojure)

    ```lua
      { import = "astrocommunity.pack.clojure" },
    ```

## Parinfer

Parinfer provides an easy to use approach that works in concert with vim-style modal editing.

The author of the code focuses on aligning code and parinfer takes care of balancing the parens.

To include new lines of code within an expression, create a new line `o` and indent.

Parinfer will move the preceeding closing paren(s) to the new line, enclosing the new code in the overall expression.

[Parinfer website](https://shaunlebron.github.io/parinfer/){target=_blank .md-button}


## Paredit

[nvim-treesitter-sexp](https://github.com/PaterJason/nvim-treesitter-sexp) will automatically manage open and close parens.

Paredit commands are provided to refactor lisp-style code and keep the parens balanced, e.g. slup, barf, promote (raise) expression, etc.

!!! EXAMPLE "Example nvim-treesitter-sexp commands"
    ```shell
    swap_prev_elem, swap_next_elem, swap_prev_form, swap_next_form, promote_elem, promote_form, splice, slurp_left, slurp_right, barf_left, barf_right
    ```

[The Animated Guide to Paredit](http://danmidwood.com/content/2014/11/21/animated-paredit.html){target=_blank .md-button}
