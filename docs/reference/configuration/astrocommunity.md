# Override Astrocommunity Configuration

Configuration in the AstroNvim Community clojure language pack can be overridden and plugins disabled to meet your needs

### Parinfer

By aligning clojure code correctly, parinfer will automatically correct the position of parenthesis and other delimiters, i.e. `()`, `[]`, `{}`

Parinfer can be disabled if preferred and the more traditional slurp/barf structural editing be done via [nvim-treesitter-sexp](#nvim-treesitter-sexp)

Include the Clojure language pack and disable the parinfer plugin by setting the plugin name to equal false

```lua
  { import = "astrocommunity.pack.clojure" },
  { "gpanders/nvim-parinfer", enabled = false },
```

### Conjure

Configure the Clojure REPL client via the conjure plugin.

> NOTE: `:help conjure-client-clojure-nrepl` for full list of Conjure options for Clojure.

Set HUD location to full width along the bottom of the screen. The HUD appears in the top right corner of the screen by default.

```lua
            ["conjure#log#hud#enabled"] = true,  -- enable HUD
            ["conjure#log#hud#width"] = 1,
            ["conjure#log#hud#anchor"] = "SE",
            ["conjure#log#botright"] = true,
```

Disable the auto repl (babashka) if an nREPL process is not listening, i.e. `.nrepl-port` file does not exist or does not contain a port number.

```lua
            -- Disable auto repl (babashka)
            ["conjure#client#clojure#nrepl#connection#auto_repl#enabled"] = false,
            ["conjure#client#clojure#nrepl#connection#auto_repl#hidden"] = true,
            ["conjure#client#clojure#nrepl#connection#auto_repl#cmd"] = nil,
            ["conjure#client#clojure#nrepl#eval#auto_require"] = false,

```

Change the test runner used by Conjure. `clojure.test` runner is used by default

- `"clojure"` clojure.test (default)
- `"clojuresCRipt" cljs.test
- `"kaocha"` lambdaisland/kaocha

```lua
            -- Set Test runner: "clojure", "clojuresCRipt", "kaocha"
            ["conjure#client#clojure#nrepl#test#runner"] = "kaocha",
```

Working example with additional configuration options to show HUD along bottom, enable auto repl if no nREPL process found and set test runner to use lambdaisland/kaocha.

```lua
  { import = "astrocommunity.pack.clojure" },
  {
    "AstroNvim/astrocore",
    opts = {
      options = {
        g = {
          -- Enable HUD and show full lenght along bottom
          ["conjure#log#hud#enabled"] = true, -- show log by default?
          ["conjure#log#hud#width"] = 1,
          ["conjure#log#hud#anchor"] = "SE",
          ["conjure#log#botright"] = true,

          -- Disable auto repl (babashka)
          ["conjure#client#clojure#nrepl#connection#auto_repl#enabled"] = false,
          ["conjure#client#clojure#nrepl#connection#auto_repl#hidden"] = true,
          ["conjure#client#clojure#nrepl#connection#auto_repl#cmd"] = nil,
          ["conjure#client#clojure#nrepl#eval#auto_require"] = false,

          -- Set Test runner: "clojure", "clojuresCRipt", "kaocha"
          ["conjure#client#clojure#nrepl#test#runner"] = "kaocha",
        },
      },
    },
  },
```

### nvim-treesitter-sexp

Treesitter based structural editing with normal mode key mappings, which can be set to false to disable. Two commands are disabled in the example.

Additional which-key keymaps can be included for greater discoverability. Example includes keymaps inspired by Spacemacs Lisp mode, `SPC k`.

```lua
  { import = "astrocommunity.pack.clojure" },
  {
    "PaterJason/nvim-treesitter-sexp",
    dependencies = {
      "AstroNvim/astrocore",
      opts = {
        -- configuration & keymaps overrides:
        -- https://github.com/PaterJason/nvim-treesitter-sexp#configuration
        -- enabled = false,  -- Set to false to disable individual keymaps
        -- set_cursor = true,
        -- keymaps = {
        -- Default key bindings - set to false to disable
        --   commands = {
        --     promote_elem = false,
        --     promote_form = false,
        --   },
        --   motions = {
        --   },
        --   textobjects = {
        --   },
        -- },
        options = {
          g = {},
        },
        mappings = {
          n = {
            -- Additional Which-key key bindings for nvim-treesitter-sexp
            ["<Leader>k"] = { name = "Structural Editing" },
            ["<Leader>kE"] = { "<Cmd>TSSexp swap_prev_elem<CR>", desc = "Swap Previous Element" },
            ["<Leader>ke"] = { "<Cmd>TSSexp swap_next_elem<CR>", desc = "Swap Previous Element" },
            ["<Leader>kF"] = { "<Cmd>TSSexp swap_prev_form<CR>", desc = "Swap Previous Form" },
            ["<Leader>kf"] = { "<Cmd>TSSexp swap_next_form<CR>", desc = "Swap Previous Form" },
            ["<Leader>kk"] = { "<Cmd>TSSexp promote_elem<CR>", desc = "Promote Element" },
            ["<Leader>kr"] = { "<Cmd>TSSexp promote_form<CR>", desc = "Promote Form" },
            ["<Leader>k@"] = { "<Cmd>TSSexp splice<CR>", desc = "Splice" },
            ["<Leader>kS"] = { "<Cmd>TSSexp slurp_left<CR>", desc = "Slurp Left" },
            ["<Leader>ks"] = { "<Cmd>TSSexp slurp_right<CR>", desc = "Slurp Right" },
            ["<Leader>kB"] = { "<Cmd>TSSexp barf_left<CR>", desc = "Barf Left" },
            ["<Leader>kb"] = { "<Cmd>TSSexp barf_right<CR>", desc = "Barf Right" },
            ["<Leader>kI"] = { "<Cmd>TSSexp barf_right<CR>", desc = "Insert Head" },
            ["<Leader>ki"] = { "<Cmd>TSSexp barf_right<CR>", desc = "Insert Tail" },
          },
          t = {
            -- terminal? mode key bindings
          },
          v = {
            -- visual mode key bindings
          },
        },
      },
    },
  },

```
