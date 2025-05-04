# 📦 Practicalli Astro Config Design

A guide to the design of AstroNvim Config created by Practicalli to support a comprehensive development workflow.

??? WARNING "Astro5 has replaced Astro as Practicalli Config for Neovim "
    [Practicalli Astro5 Configuration](/neovim/install/astro5-configuration.md)



## Files overview

The file structure as taken from the AstroNvim template and new files were created to minimise changes, making it simpler to add updates from the original template repository.

!!! INFO "Key - AstroNvim template file changes"
    Icons describing if a file was added, changed or unchanged from the [AstroNvim template](https://github.com/AstroNvim/template)

    - :octicons-file-16: unchanged
    - :octicons-file-diff-16: changed
    - :octicons-file-added-16: added
    - :material-close-circle-outline: config not activated (comment `if` statement to activate)


:octicons-file-16: `init.lua` ensures the Lazy package manager is available when Neovim starts up. This file is unchanged from the AstroNvim template.

:octicons-file-diff-16: `lua/lazy_setup.lua` configures the Lazy package manager.  `zipPlugin` enabled to support Clojure docs and source navigation inside libraries.

:octicons-file-diff-16: `lua/community.lua` imports plugin configurations from AstroCommunity, including the Clojure pack.

:octicons-file-16: :material-close-circle-outline: `lua/polish.lua` general lua configuration loaded after AstroNvim configs.

`lua/plugins/` for additional plugins organised logically. All `.lua` files are automatically loaded from this directory when starting Neovim.

- :octicons-file-16: :material-close-circle-outline: `astrocore.lua`, `astrolsp.lua`, `astroui.lua` examples of overriding AstroNvim defaults
- :octicons-file-added-16: `clojure.lua` alternative approach to configure clojure, extending the AstroNvim Clojure pack
- :octicons-file-added-16: `github.lua` issue & PR management with octo.nvim (requires GitHub CLI)
- :octicons-file-16: :material-close-circle-outline: `mason.lua` ensure tools are installed by default (LSP servers, format & lint tools, DAP debug tools)
- :octicons-file-16: :material-close-circle-outline: `neo-tree.lua` visual file navigator - example config
- :octicons-file-16: :material-close-circle-outline: `none-ls.lua` example config for format & lint tools
- :octicons-file-added-16: :material-close-circle-outline: `platuml.lua` UML diagrams defined with code - requires plantuml.com install
- :octicons-file-added-16: `snippets.lua` load JSON style snippet definitions
- :octicons-file-added-16:`telescope.lua` ensure Treesitter languages are installed (AstroCommunity language packs also ensure parsers installed)
- :octicons-file-16: :material-close-circle-outline: `treesittter.lua` ensure Treesitter languages are installed (AstroCommunity language packs also ensure parsers installed)
- :octicons-file-16: :material-close-circle-outline: `user.lua` example user configuration, added via `lua/plugins/user-practicalli.lua`
- :octicons-file-added-16: `user-practicalli.lua` theme, dashboard & key binding preferences enjoyed by Practicalli
- :octicons-file-added-16: `user-termux.lua` mason lsp server overrides, pinned plugin versions for neovim 0.9.x


## Disable Plugins

Practicalli Astro provides a rich set of Neovim plugins.  Any plugin can be configured as disabled, usually in a user configuration, e.g. `lua/plugins/user-practicalli.lua`

!!! EXAMPLE "Disable parinfer and sexp plugins"
    ```lua title="lua/plugins/user-practicalli.lua"
      -- ----------------------------------------------
      { "nvim-parinfer", enabled = false },
      { "nvim-treesitter-sexp", enabled = false },
      -- ----------------------------------------------
    ```


## Clojure support

The [:fontawesome-brands-github: AstroCommunity](https://github.com/AstroNvim/astrocommunity/) provides a Clojure language pack that ensures `clojure` Treesitter parser and `clojure-lsp` support and installed automatically.

The pack contains 4 Neovim plugins:

- conjure REPL client to evaluate code
- nvim-parinfer code indenting structural editing
- nvim-treesitter-sexp paredit (slurp/barf etc) structural editing
- ts-comment.nvim Clojure comment patterns


!!! INFO: "Practicalli AstroNvim Config includes Clojure pack"


=== "AstroCommunity Clojure Pack"

    Edit the `plugins/community.lua` file and import the Clojure pack.  The `"AstroNvim/astrocommunity",` repository is already added to to the file.

    ```lua
    -- Packs
    -- Treesitter: clojure , Lsp: clojure-lsp, Lint/format:
    { import = "astrocommunity.pack.clojure" },
    ```

    ??? HINT "Exclude a plugin from the pack"
        The Clojure pack includes parinfer and paredit tools for structural editing, which both work together without issue.  Should one or both of these plugins not be reqiured, set enabled to false
        ```lua
        return {
          "AstroNvim/astrocommunity",
          { import = "astrocommunity.pack.clojure" },
          { "gpanders/nvim-parinfer", enabled = false },
        ```

    !!! EXAMPLE "Override Conjure configration"
        Add the AstroCommunity Clojure pack and additional configuration to create a tailored experience

        `:help conjure` for general Conjure options.

        `:help conjure-client-clojure-nrepl` for Clojure specific options.

        ```lua
        return {
          "AstroNvim/astrocommunity",
          { import = "astrocommunity.pack.clojure" },
          {
            "AstroNvim/astrocore",
            opts = {
              options = {
                g = {
                  -- show HUD REPL log at startup
                  ["conjure#log#hud#enabled"] = false,

                  -- Hightlight evaluated forms
                  -- ["conjure#highlight#enabled"] = true,

                  -- Trim log after number of lines. Default: `10000`
                  -- ["conjure#log#trim#at"] = 200,
                  -- Trim log to number of lines. Default: `7000`
                  -- ["conjure#log#trim#to"] = 100,

                  -- auto repl (babashka)
                  ["conjure#client#clojure#nrepl#connection#auto_repl#enabled"] = false,
                  ["conjure#client#clojure#nrepl#connection#auto_repl#hidden"] = true,
                  ["conjure#client#clojure#nrepl#connection#auto_repl#cmd"] = nil,
                  ["conjure#client#clojure#nrepl#eval#auto_require"] = false,

                  -- Test runner: "clojure", "clojuresCRipt", "kaocha"
                  ["conjure#client#clojure#nrepl#test#runner"] = "kaocha",
                },
              },
            },
          },
        }
        ```

    ??? INFO "Config comment for parinfer"
        The parinfer comment configuration may not be required when using ts-comment.nvim to set the Clojure comment pattern.
        ```lua
        {
          "gpanders/nvim-parinfer",
          filetype = { "clojure" },
          config = function()
            vim.g.parinfer_force_balance = true
            vim.g.parinfer_comment_chars = ";;"
          end,
        },
        ```

=== "Manually add plugins"
    Add Conjure and parinfer plugin that will load when Clojure or Fennel file is opened.
    !!! EXAMPLE "Clojure Packages in AstroNvim user configuration"
            ```lua title=".config/astronvim-config/plugins/clojure.lua"
            -- Lazy Package manager configuration
            return {
              {
                "Olical/conjure",
                -- load plugin on filetypes
                ft = { "clojure", "fennel" },
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

    !!! HINT "Manual install of Treesitter Clojure Parser"
        `:TSInstall clojure` in Neovim will install the parser. A parser not included in the `opts.ensure_installed` configuration must be updated manually each time treesitter plugin is updated


??? HINT "Switch to Parinfer Parens mode for Paredit structural editing"
    Changing the Parinfer mode to `paren` gives a structured editing experience similar to Paredit (or Smartparens).

    Add the following configuration within the `return {}` table in the `plugins/community.lua` file to set the parinfef mode, i.e. `paren`, `smart` or `indent` (default

    ```lua title="plugins/community.lua"
      {
        "gpanders/nvim-parinfer",
        ft = { "clojure" },
        config = function()
          vim.g.parinfer_force_balance = true
          vim.g.parinfer_comment_chars = ";;"
          vim.g.parinfer_mode = "paren"
        end,
      },
    ```


### Clojure Mappings

Conjure mappings are defined respective to a `<localleader>` value. Define a local leader in the AstroNvim user configuration, e.g. `,` and all Conjure mappings become available.

??? INFO "AstroNvim 3.17.0 has localleader"
    AstroNvim 3.17.0 release sets `localleader` to `,` so a separate setting is not required in the user configuration (unless a different localleader is preferred)

??? EXAMPLE "Set localleader in user config"
    `options.lua` in the user configuration provides a consistent way to set Neovim options.

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


## Clojure LSP

Clojure LSP support is enabled via the AstroCommunity Clojure pack.

`clojure_lsp` can be added using Mason UI, `SPC p m` or in the `plugins/mason.lua` file

??? EXAMPLE "Manual user config of clojure lsp server"
    ```lua
    -- customize mason plugins
    return {
      -- use mason-lspconfig to configure LSP installations
      {
        "williamboman/mason-lspconfig.nvim",
        -- overrides `require("mason-lspconfig").setup(...)`
        opts = function(_, opts)
          -- add more things to the ensure_installed table protecting against community packs modifying it
          opts.ensure_installed = require("astronvim.utils").list_insert_unique(opts.ensure_installed, {
            -- "clojure_lsp",  -- provide by Clojure pack
            "marksman", -- Markdown structure (also in markdown pack)
            "yamlls",
          })
        end,
      },
    }
    ```


## Snippets

The AstroNvim user example includes a commented LuaSnip configuration

!!! EXAMPLE "LuaSnip with json format snippets in `snippets/` directory"
    ```lua title=".config/astronvim-config/plugins/core.lua"
    return {
      --LuaSnip with json format snippets in `snippets/` directory
      {
        "L3MON4D3/LuaSnip",
        config = function(plugin, opts)
          require "astronvim.plugins.configs.luasnip"(plugin, opts) -- include the default astronvim config that calls the setup call
          -- add more custom luasnip configuration such as filetype extend or custom snippets
          require("luasnip.loaders.from_vscode").lazy_load { paths = { "./snippets" } } -- include JSON style snippets
          local luasnip = require "luasnip"
          luasnip.filetype_extend("javascript", { "javascriptreact" })
        end,
      },
    }
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
      -- Import each plugin from the Astro Community as required
      { import = "astrocommunity.editing-support.todo-comments" },
      { import = "astrocommunity.git.neogit" },
      { import = "astrocommunity.git.octo" },
      { import = "astrocommunity.git.openingh" },
    }
    ```

AstroCommunity packs set up support for each language

!!! EXAMPLE "Language packs enabled in Practicalli AstroNvim Config"
    ```lua title=".config/astronvim-config/plugin/community.lua"
      -- Packs
      -- Treesitter: dockerfile , Lsp: dockerls & docker_compose_language_service, Lint/format: hadolint
      { import = "astrocommunity.pack.docker" },
      -- Treesitter: json & jsonc, Lsp: jsonls, Lint/format: stylua
      { import = "astrocommunity.pack.json" },
      -- Treesitter: lua, Lsp: lua_ls, Lint/format: stylua
      { import = "astrocommunity.pack.lua" },
      -- Treesitter: markdown & markdown_inline, Lsp: marksman, Lint/format: prettierd
      -- Pack disabled as prettierd too agressive with format
      -- { import = "astrocommunity.pack.markdown" },
      -- Treesitter: markdown & markdown_inline, Lsp: marksman, Lint/format: prettierd
      { import = "astrocommunity.pack.yaml" },
    ```


## Themes

Themes are a collection of one or more colorschemes to affect the apperance of text, icons, highlights, etc.

Themes supporting `vim.opt.background` can change between dark and light colorscheme (`SPC u b` UI > background in AstroNvim)

`SPC f t` selector shows themes colorschemes, as long as the themes are configured to disable lazy loading

The default `astrodark` theme is set via the `colorscheme` option in `init.lua`

[Everforest](https://github.com/sainnhe/everforest) provides a good dark and light theme and supports the background option to toggle between each colorscheme.

!!! EXMAPLE "Practicalli AstroNvim Config - default theme"
    ```lua
      {
        -- AstroUI provides the basis for configuring the AstroNvim User Interface
        -- Configuration documentation can be found with `:h astroui`
        "AstroNvim/astroui",
        ---@type AstroUIOpts
        opts = {
          colorscheme = "everforest",
        },
      },
    ```

[:fontawesome-brands-github: AstroCommunity themes](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/colorscheme){target=\_blank .md-button}


### Configure Lazy plugins

[:globe_with_meridians: Lazy.nvim Plugin specification](https://github.com/folke/lazy.nvim#-plugin-spec){target=\_blank .md-button}


## Config Format and Lint tools

!!! HINT "Disable format on save when tools provide unexpected results"
    `SPC u f` toggles if the respective format tool should run for the current buffer.  `SPC u F` for all buffers of the current kind.

    `init.lua` lsp section can enable or disable format on save for specific file types.

Mason is responsible for installing lint and format tools

null-ls is responsible for running each tool and provides default configuration for code_actions, completion, diagnostics, formatting and hover.

[:globe_with_meridians: null-ls built-in configuration](https://github.com/jose-elias-alvarez/null-ls.nvim/tree/main/lua/null-ls/builtins){target=_blank .md-button}

!!! WARNING "Override config file unconsistent"
    The configuration file defined by `-config-path` does not always seem to be used when running astronvim.  Quit and start Neovim again seems to use the configuration file.

??? EXAMPLE "Override null-ls builtin configuration"
    Specify configuration files to use that override the null-ls builtin configuration

    ```lua  hl_lines="9 10 11 12"
    return {
      "jose-elias-alvarez/null-ls.nvim",
      opts = function(_, config)
        -- config variable is the default configuration table for the setup function call
        local null_ls = require "null-ls"
        config.sources = {
          null_ls.builtins.formatting.markdownlint.with {
            -- pass arguments to modify/override the null-ls builtin configuration
            extra_args = {
              "--config-path",
              vim.fn.expand("~/.config/astro-config/tool-config/markdownlint.yaml") },
          },
        }
        return config -- return final config table
      end,
    }
    ```
    > `vim.fn.expand()` reports luacheck error `accessing undefined variable` but seems to work regardless


??? EXAMPLE "General configuration for LSP Servers"
    ```lua hl_lines="14 15 16 17" title=".config/astronvim-config/init.lua"
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

## Override Key binding

AstroNvim uses Lazy package manager to set keys for packages.

Astrocommunity configuration defines a `keys` table that is used by Lazy.

In the user configuration, return a function that sets key bindings to overide the `keys` table provided by astrocommunity

??? EXAMPLE "Override Key bindings for vim highlighter"
    ```lua title=".config/astronvim-config/plugins/community.lua"
    {
        "vim-highlighter",
        keys = function()
            return {
                { "<leader>nn", "<cmd>Hi><CR>", desc = "Next Recently Set Highlight" },
                { "<leader>ng", "<cmd>Hi<<CR>", desc = "Previous Recently Set Highlight" },
                { "<leader>n[", "<cmd>Hi{<CR>", desc = "Next Nearest Highlight" },
                { "<leader>n]", "<cmd>Hi}<CR>", desc = "Previous Nearest Highlight" },
            }
        end,
    }
    ```

## Plugin Key binding

Add key binding if a plugin is available wrapped in an if statement, when defining keys in a different place to adding the plugin, e.g whichkey mappings.lua

```lua
if is_available "plugin-name" then
  ,,,
else
```


<!--


# Config Design - AstroNvim

[:globe_with_meridians: AstroNvim](https://astronvim.com/) is a community configuration with an engaging UI, using Lazy for plugin management (Neovim packages) and Mason for package management (LSP, DAP, format and lint tools)

[:fontawesome-brands-github: Practicalli AstroNvim User Config](https://github.com/practicalli/astro) is a user configuration that extends AstroNvim and imports packages from the [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/user_example).

Practicalli AstroNvim User Config provides a complete Clojure config on top of AstroNvim.


!!! WARNING "Page being rewritten"

## Template desing


## Practicalli Changes


## Practicalli Additions


### User file

Lua files under `lua/plugins/` load in alphabetical order.  Each configuration file should be independent from each other.

A `lua/plugins/user-name.lua` file is an approprate place to override plugin defaults, as it will be the last configuration file to load.


## Adding Your own Plugins

- create a `lua/plugins/plugin-name.lua` with all the configuration and key mappings
- add to a `lua/plugins/user-name.lua`

- community.lua when using a Plugin Config from Astro Community

Review the `lua/plugins/example-config.lua` file for examples of adding and configuring plugins


### Add LSP DAP Lint and Format tools

`SPC p m` to launch Mason which manages LSP servers, linters, filters ...

![AstroNvim packages - mason all installed](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-packages-mason-installed-all.png?raw=true){loading=lazy}


### Configure format rules

The configuration files for each lint and format tool should be used by Neovim.

> Setting a different location for these files has proved challenging.  `plugin/null-ls.lua` has a section to override its builtin configuration for each lint and format tool, however, in tests Practicalli was unable to succeffuly set a different location.


-->



<!--

## Telescope Extensions

AstroNvim Extensions

- [aerial.nvim](https://github.com/stevearc/aerial.nvim)

  - `SPC l s` to search symbols
  - `SPC l S` to list symbols or :AerialToggle

- autocommands - :Telescope autocommands - lists autocommands, e.g comment_lines custom for Clojure
- builtin :Telescope builtin - lists AstroNvim builtin telescope extensions (not user added extensions)
- buffers `SPC f b` - selection from currently open buffers
- commands :Telescope commands - selection of all neovim commands
- command_history :Telescope command_history - selection of previous commands, run selected command
- current_buffer_fuzzy_find - uses deprecated API, removed in 0.10
- current_buffer_tags - ctags
- diagnostics - `SPC l D` workspace diagnostics, from LSP server
- fd - `SPC f f` Find files - same as find_files ?
- filetypes
- find_files - `SPC f f` find files
- fzf - Error: command.lua 193 attempt to call a nil value
- git_bcommits ??
- git_commits `SPC g c` list
- git_files
- git_stash
- git_status git status for project - use lazygit or neogit instead
- help_tags
- highlights colour hightlights for annotations, notes, etc (for desiging a theme?)
- jumplist selector listing previous places that can be jumped to.. is this from the community plugin?
- keymaps `SPC f k` selector for all key bindings known to neovim config
- live_grep
- loclist
- lsp_definitions
- lsp_dynamic_workspace_symbols
- lsp_document_symbols
- lsp_implementations
- lsp_incoming_calls
- lsp_outgoing_calls
- lsp_references
- lsp_type_definitions
- man_pages
- marks
- notify browse notification messages
- oldfiles
- pickers
- planets selector for pictures of planets (very pixelated pictures)
- quickfix
- reloader
- registers `SPC f r` selector for neovim registers (paste value from register to current cursor location)
- search_history
- spell_suggest
- symbols Error: sources not found (need to create your own symbols?)
- tagstack
- treesitter - nothing happens
- vim_options `vim.opts` options including settabline configured in user config.

AstroCommunity

- projects

Other extensions

- telescope-env.nvim
- <https://github.com/ANGkeith/telescope-terraform-doc.nvim>
- <https://github.com/olacin/telescope-cc.nvim>
- <https://github.com/gbprod/yanky.nvim>
- <https://github.com/smartpde/telescope-recent-files>
- <https://github.com/nvim-telescope/telescope-file-browser.nvim>
- <https://github.com/lpoto/telescope-docker.nvim>
- <https://github.com/prochri/telescope-all-recent.nvim>
- <https://github.com/nvim-telescope/telescope-frecency.nvim>
- <https://github.com/barrett-ruth/telescope-http.nvim>
- <https://github.com/pwntester/octo.nvim>
- <https://github.com/AckslD/nvim-neoclip.lua>


## Review

- <https://github.com/datamonsterr/astronvim_config>



-->
