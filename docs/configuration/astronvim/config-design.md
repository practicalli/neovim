# Practicalli AstroNvim Configuration

A guide to the AstroNvim Config user configuration created by Practicalli to support Clojure development.


## Add Clojure support

Set a local leader for Conjure to add its key bindings too

`options.lua` in the user configuration provides a consistent way to define variables to set Neovim options.

!!! EXAMPLE "Clojure Packages in AstroNvim user configuration"
    ```lua hl_lines="13" title=".config/astronvim-config/options.lua"
    -- set vim options here (vim.<first_key>.<second_key> = value)
    return {
      opt = {
        -- set to true or false etc.
        relativenumber = true, -- sets vim.opt.relativenumber
        number = true,         -- sets vim.opt.number
        spell = false,         -- sets vim.opt.spell
        signcolumn = "auto",   -- sets vim.opt.signcolumn to auto
        wrap = false,          -- sets vim.opt.wrap
      },
      g = {
        mapleader = " ",                 -- sets vim.g.mapleader
        maplocalleader = ",",            -- Set local leader key binding (supports Conjure key bindings)
        autoformat_enabled = true,       -- enable or disable auto formatting at start (lsp.formatting.format_on_save must be enabled)
        cmp_enabled = true,              -- enable completion at start
        autopairs_enabled = true,        -- enable autopairs at start
        diagnostics_mode = 3,            -- set the visibility of diagnostics in the UI (0=off, 1=only show in status line, 2=virtual text off, 3=all on)
        icons_enabled = true,            -- disable icons in the UI (disable if no nerd font is available, requires :PackerSync after changing)
        ui_notifications_enabled = true, -- disable notifications when toggling UI elements
        VM_leader = "gm"                 -- Visual Multi Leader (multiple cursors)
      },
    }
    ```

Add Conjure plugin that will load when Clojure, Fennel or Python file is opened.

!!! EXAMPLE "Clojure Packages in AstroNvim user configuration"
    ```lua title=".config/astronvim-config/init.lua"
    -- Local variables
    local lisp_dialects = { "clojure", "fennel" }

    -- Lazy Package manager configuration
    return {
      {
        "Olical/conjure",
        -- load plugin on filetypes
        ft = { "python", unpack(lisp_dialects) },
      },
    }
    ```

Improve syntax highlighting by installing the Clojure parser for Treesitter.

!!! EXAMPLE "Treesitter Parser for clojure in AstroNvim user configuration"
    ```lua hl_lines="7" title=".config/astronvim-config/plugins/treesitter.lua"
    return {
      "nvim-treesitter/nvim-treesitter",
      opts = function(_, opts)
        -- add more things to the ensure_installed table protecting against community packs modifying it
        opts.ensure_installed = require("astronvim.utils").list_insert_unique(opts.ensure_installed, {
          -- "lua"
        "clojure"
        })
      end,
    }
    ```

!!! HINT "Install Treesitter Clojure Parser manually"
    `:TSInstall clojure` in Neovim will install the parser.  A parser not included in the `opts.ensure_installed` configuration must be updated manually each time treesitter plugin is updated

## Snippets

The AstroNvim user example includes a commented LuaSnip package code.

```lua title=".config/astronvim-config/plugins/core.lua"
  -- {
  --   "L3MON4D3/LuaSnip",
  --   config = function(plugin, opts)
  --     require "plugins.configs.luasnip" (plugin, opts)  -- include the default astronvim config that calls the setup call
  --     -- add more custom luasnip configuration such as filetype extend or custom snippets
  --     local luasnip = require "luasnip"
  --     luasnip.filetype_extend("javascript", { "javascriptreact" })
  --   end,
  -- },
```

AstroNvim includes a [Recipe for custom snippets](https://astronvim.com/Recipes/snippets)

```lua
return {
  plugins = {
    {
      "L3MON4D3/LuaSnip",
      config = function(plugin, opts)
        require "plugins.configs.luasnip"(plugin, opts) -- include the default astronvim config that calls the setup call
        require("luasnip.loaders.from_vscode").lazy_load { paths = { "./lua/user/snippets" } } -- load snippets paths
      end,
    },
  },
}
```

Practicalli AstroNvim Config combines the two examples to get

!!! EXAMPLE "AstroNvim config with custom VS Code style snippets"
    ```lua title=".config/astronvim-config/plugins/core.lua"
      {
        "L3MON4D3/LuaSnip",
        config = function(plugin, opts)
          require "plugins.configs.luasnip" (plugin, opts)                                       -- include the default astronvim config that calls the setup call
          -- add more custom luasnip configuration such as filetype extend or custom snippets
          require("luasnip.loaders.from_vscode").lazy_load { paths = { "./lua/user/snippets" } } -- load snippets paths
          local luasnip = require "luasnip"
          luasnip.filetype_extend("javascript", { "javascriptreact" })
        end,
      },

```

## AstroNvim Community packages

[:globe_with_meridians: AstroNvim Community](https://github.com/AstroNvim/astrocommunity){target=\_blank} provides a large number of packages currated by the community.

Visit the AstroNvim Community repository on GitHub and browse the packages available.

`import` each package of interest to the `plugins/community.lua` file in the AstroNvim user configuration.

!!! EXAMPLE "AstroNvim Community Packages in AstroNvim user configuration"
    ```lua title=".config/astronvim-config/plugins/community.lua"
    return {
      -- Add the community repository of plugin specifications
      "AstroNvim/astrocommunity",

      { import = "astrocommunity.editing-support.todo-comments" },
      { import = "astrocommunity.git.neogit" },
      { import = "astrocommunity.git.octo" },
      { import = "astrocommunity.git.openingh" },
    }
    ```

## Themes

Use themes that support the `vim.opt.background` command to change between dark and light themes (`SPC u b` UI > background in AstroNvim)
Variant respects , using dawn when light and dark_variant when dark

Available via AstroCommunity

- [gruvbox.nvim](https://github.com/ellisonleao/gruvbox.nvim/) - requires highlight setting in user config
- [rose-pine](https://github.com/rose-pine/neovim)
- [oxocarbon.nvim](https://github.com/nyoom-engineering/oxocarbon.nvim) (written in Fennel)

<!-- 
  -- Theme testing for visual appeal:
  -- colorscheme = "astrodark",  (default theme, no background support I think)
  -- colorscheme = "catppuccin",   -- light color to pale, lacks contrast
  -- colorscheme = "dayfox",
  colorscheme = "everforest",
  -- colorscheme = "github_light",  -- no background support, otherwise quite nice
  -- colorscheme = "gruvbox",  -- status and tablines inverted - doesnt look good
  -- colorscheme = "gruvbox-baby", -- no background support
  -- colorscheme = "kanagawa",  -- nice
  -- colorscheme = "onigiri",  -- nice
  -- colorscheme = "oxocarbon",
  -- colorscheme = "rose-pine", -- light colour very bright
-->

### Configure Lazy plugins

[:globe_with_meridians: Lazy.nvim Plugin specification](https://github.com/folke/lazy.nvim#-plugin-spec){target=_blank .md-button}


## Review

- https://github.com/datamonsterr/astronvim_config


<!-- 
### Format and Lint tool configuration

Mason is responsible for installing packages

null-ls is responsible for running each tool and provides default configuration for code_actions, completion, diagnostics, formatting and hover.

[:globe_with_meridians: null-ls built-in configuration](https://github.com/jose-elias-alvarez/null-ls.nvim/tree/main/lua/null-ls/builtins){target=_blank .md-button}

??? EXAMPLE "Override null-ls builtin configuration"
    Specify configuration files to use that override the null-ls builtin configuration

    ```lua  hl_lines="16 17 18 19"
    return {
      "jose-elias-alvarez/null-ls.nvim",
      opts = function(_, config)
        -- config variable is the default configuration table for the setup function call
        local null_ls = require "null-ls"
        -- Check supported formatters and linters
        -- <https://github.com/jose-elias-alvarez/null-ls.nvim/tree/main/lua/null-ls/builtins/formatting>
        -- <https://github.com/jose-elias-alvarez/null-ls.nvim/tree/main/lua/null-ls/builtins/diagnostics>
        config.sources = {
          -- Set a formatter
          -- null_ls.builtins.formatting.stylua,
          -- null_ls.builtins.formatting.prettier,
          null_ls.builtins.formatting.markdownlint.with {
            -- pass arguments to modify the null-ls builtin configuration
            extra_args = {
              "--config ",
              "/home/practicalli/.markdownlint.yaml",
            },
          },
          null_ls.builtins.formatting.cljstyle.with {
            -- use my own configuration rules
            args = {
              "--config ",
              "/home/practicalli/.config/.cljstyle",
            },
          },
        }
        return config -- return final config table
      end,
    }
    ```

??? EXAMPLE "General configuration for LSP Servers"
    ```lua hl_lines="17" title=".config/astronvim-config/init.lua"
      lsp = {
        -- customize lsp formatting options
        formatting = {
          -- control auto formatting on save
          format_on_save = {
            enabled = true,     -- format on save globally
            allow_filetypes = { -- format on save for specified filetypes only
              -- "go",
            },
            ignore_filetypes = { -- turn off format on save for specified filetypes
              -- "python",
            },
          },
          disabled = { -- switch off formatting capabilities for the listed language servers
            -- turn off lua_ls formatting capability if you want to use StyLua to format your lua code
            -- "lua_ls",
            -- "markdownlint",
          },
          timeout_ms = 1000, -- default format timeout
          -- filter = function(client) -- fully override the default formatting function
          --   return true
          -- end
        },
        -- enable servers that you already have installed without mason
        servers = {
          -- "pyright"
        },
      },
    ```


!!! WARNING "Configuring rules for linters"
    AstroNvim uses null-ls to format files (trigged by save - althought that is configurable).  So far practicalli has not figured out how to successfully configure rules used by linters

    `~/.config/astronvim-config/plugins/null-ls.lua` should take `extra-args` section that can be used to pass command line args, e.g. specifying a configuration file to use for a linter.  This did not work when tried with markdownlint 
-->
