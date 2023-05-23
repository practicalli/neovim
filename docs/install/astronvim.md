# AstroNvim

AstroNvim is a community configuration with a very engaging UI, using Lazy for plugin management (Neovim packages) and Mason for package management (LSP, DAP, format and lint tools)

## Prerequisits

- Nerd Fonts version 3 (breaking changes between version 2 and 3)

## Clone AstroNvim

Clone AstroNvim repository to either

- `$HOME/.config/astronvim/` when using multiple configurations 
- `$HOME/.config/nvim` if only ever using one configuration.

## Clone AstroNvim user config

AstroNvim provides a [:fontawesome-brands-github: template repository](https://github.com/AstroNvim/user_example) to create a user configuration. The template includes [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/user_example) configuration to make it easier to extend the feature of AstroNvim.

=== "Practicalli AstroNvim Config"
    Clone the [:fontawesome-brands-github: Practicalli AstroNvim config](https://github.com/practicalli/astronvim-config) which provides a user configuration with [Clojure support](clojure.md)
    !!! NOTE ""
        ```shell
        git clone <http://github.com/practicalli/astronvim-config> $HOME/.config/astronvim/lua/user
        ```
    Or clone to a separate directory and create a symbolic link 
    !!! NOTE ""
        ```shell
        git clone <http://github.com/practicalli/astronvim-config> $HOME/.config/astronvim/lua/user \
        ln -s $HOME/.config/astronvim-config/ $HOME/.config/astronvim/lua/user
        ```

=== "AstroNvim User Config"
    Create your own user configuration using the AstroNvim user configuration template repository.

    Create a repository from the AstroNvim/user_example repository template

    ![AstroNvim user example repository - use this template](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-user-config-template-github-repository.png?raw=true){loading=lazy}

    Clone the newly created repository into the existing AstroNvim configuration, in a `user` directory
    ```shell
    git clone git@github.com/<github-account>/<new-repository> $HOME/.config/astronvim/lua/user
    ```

## Install packages

`SPC p m` to launch Mason which manages LSP servers, linters, filters ...

![AstroNvim packages - mason all installed](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-packages-mason-installed-all.png?raw=true){loading=lazy}


### Configure format rules

Mason is responsible for installing packages and null-ls seems responsible for running each tool, with (assumption: null-ls running the tools with built-in configuration)

??? EXAMPLE "General configuration for LSP Servers"
    Disable format capabilities of markdownlint (until rules that conflict with MkDocs formatting can be configured) 
    ```lua hl_lines="17" title=".config/astronvim-config/init.lua"
      lsp = {
        -- customize lsp formatting options
        formatting = {
          -- control auto formatting on save
          format_on_save = {
            enabled = true,     -- enable or disable format on save globally
            allow_filetypes = { -- enable format on save for specified filetypes only
              -- "go",
            },
            ignore_filetypes = { -- disable format on save for specified filetypes
              -- "python",
            },
          },
          disabled = { -- disable formatting capabilities for the listed language servers
            -- disable lua_ls formatting capability if you want to use StyLua to format your lua code
            -- "lua_ls",
            "markdownlint",
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


- markdown
  - line lenght 240
  - dont apply fixes (mkdocs indenting for tabs causing last line to be formatted to start of line, breaking mkdocs)

!!! WARNING "Configuring rules for linters"
    AstroNvim uses null-ls to format files (trigged by save - althought that is configurable).  So far practicalli has not figured out how to successfully configure rules used by linters

    `~/.config/astronvim-config/plugins/null-ls.lua` should take `extra-args` section that can be used to pass command line args, e.g. specifying a configuration file to use for a linter.  This did not work when tried with markdownlint 

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

!!! EXAMPLE "AstroNvim user example"
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


### Configure Lazy plugins

[:globe_with_meridians: Lazy.nvim Plugin specification](https://github.com/folke/lazy.nvim#-plugin-spec){target=_blank .md-button}
