# 📦 Practicalli AstroNvim Config Design

A guide to the AstroNvim Config user configuration created by Practicalli to support Clojure development.

??? INFO "AstroCommunity used where possible"
Plugins and configuration is added vial AstroCommunity were possible, to minimise the code size and maintenance of the configuration

 
## User Config overview

`core.lua` is for tuning plugins shipped with astronvim config

`plugins/` for additional plugins organised logically. All `.lua` files are read from this directory 

- `user.lua` for general user defined plugins
- `clojure.lua` adds Conjure and parinf, ensuring Clojure treesitter parser and Clojure LSP
    

## Clojure support

The [:fontawesome-brands-github: AstroCommunity](https://github.com/AstroNvim/astrocommunity/) provides a Clojure language pack that adds Conjure and nvim-parinfer, along with `clojure` Treesitter parser and `clojure-lsp` support.

=== "AstroCommunity Pack"

    Edit the `plugins/community.lua` file and import the Clojure pack.  The `"AstroNvim/astrocommunity",` repository is already added to to the file.

    ```lua
    -- Packs
    -- Treesitter: clojure , Lsp: clojure-lsp, Lint/format:
    { import = "astrocommunity.pack.clojure" },
    ```

=== "Override AstroCommunity Pack"

    Create a `plugins/clojure.lua` file and add the AstroCommunity repository, Clojure pack and additional configuration to your own preferences
    ??? EXAMPLE "Clojure configuration with user configration overrides"
        ```lua
        return {
          "AstroNvim/astrocommunity",
          { import = "astrocommunity.pack.clojure" },
          {
            "Olical/conjure",
            -- load plugin on filetypes
            ft = { "clojure", "fennel" },
            config = function()
              -- HUD
              -- Example: Set to `"SE"` and HUD width to `1.0` for full width HUD at bottom of screen
              vim.g["conjure#log#hud#width"] = 1 -- Width of HUD as percentage of the editor width, 0.0 and 1.0.
              vim.g["conjure#log#hud#enabled"] = false -- Display HUD
              vim.g["conjure#log#hud#anchor"] = "SE" -- Preferred corner position for the HUD
              vim.g["conjure#log#botright"] = true -- Open log at bottom or far right of editor
              -- REPL
              vim.g["conjure#extract#context_header_lines"] = 100 -- Number of lines to check for `ns` form
              vim.g["conjure#client#clojure#nrepl#connection#auto_repl#enabled"] = false -- ;; Start "auto-repl" process, eg. babashka
              vim.g["conjure#client#clojure#nrepl#connection#auto_repl#hidden"] = true -- ;; Hide auto-repl buffer when triggered
              vim.g["conjure#client#clojure#nrepl#connection#auto_repl#cmd"] = nil -- ;; Command to start the auto-repl
              -- ;; Automatically require namespace of new buffer or current buffer after connection
              vim.g["conjure#client#clojure#nrepl#eval#auto_require"] = false
              -- Reloading code
              -- Function to call on refresh (reloading) the log, namespace-qualified name of a zero-arity
              -- vim.g["conjure#client#clojure#nrepl#refresh#after"] = nil
              -- The namespace-qualified name of a zero-arity function to call before reloading.
              -- vim.g["conjure#client#clojure#nrepl#refresh#before"] = nil
              -- List of directories to scan. If no directories given, defaults to all directories on the classpath.
              -- vim.g["conjure#client#clojure#nrepl#refresh#dirs"] = nil
              -- Testing
              -- ;; Test runner called from the test key mappings
              vim.g["conjure#client#clojure#nrepl#test#runner"] = "kaocha"
              -- Print raw test evaluation result, suppressing prefix for stdout lines `; (out)`
              -- vim.g["conjure#client#clojure#nrepl#test#raw_out"] = nil
              -- Override string appended to the end of the test runner calls
              -- vim.g["conjure#client#clojure#nrepl#test#call_suffix"] = nil
            end
          },
          {
            "gpanders/nvim-parinfer",
            ft = lisp_dialects,
            config = function()
              vim.g.parinfer_force_balance = true
              vim.g.parinfer_comment_chars = ";;"
            end,
          },
        }
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

              {
                "gpanders/nvim-parinfer",
                ft = { "clojure", "fennel" },
                config = function()
                  vim.g.parinfer_force_balance = true
                  vim.g.parinfer_comment_chars = ";;"
                end,
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
        `:TSInstall clojure` in Neovim will install the parser. A parser not included in the `opts.ensure_installed` configuration must be updated manually each time treesitter plugin is updated


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
        require "plugins.configs.luasnip" (plugin, opts) -- include the default astronvim config that calls the setup call
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

> TODO: Submit a pull request with a Clojure pack to the AstroCommunity


## Themes

Themes are a collection of one or more colorschemes to affect the apperance of text, icons, highlights, etc.

Themes supporting `vim.opt.background` can change between dark and light colorscheme (`SPC u b` UI > background in AstroNvim)

`SPC f t` selector shows themes colorschemes, as long as the themes are configured to disable lazy loading

The default `astrodark` theme is set via the `colorscheme` option in `init.lua`

[Everforest](https://github.com/sainnhe/everforest) provides a good dark and light theme and supports the background option to toggle between each colorscheme.

!!! EXMAPLE "Practicalli AstroNvim Config - default theme"
    ```lua
    colorscheme = "everforest",
    ```

[:fontawesome-brands-github: AstroCommunity themes](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/colorscheme){target=\_blank .md-button}

!!! EXMAPLE "Practicalli AstroNvim Config themes"
    ```lua
    return {
    {
    "AstroNvim/astrotheme", -- default AstroNvim theme
    lazy = false,
    },
      -- Add the community repository of plugin specifications
      "AstroNvim/astrocommunity",
      { import = "astrocommunity.colorscheme.everforest" },
      {
        "sainnhe/everforest",
        lazy = false,
      },
      { import = "astrocommunity.colorscheme.nightfox-nvim" },
      {
        "EdenEast/nightfox.nvim",
        lazy = false,
      },
      { import = "astrocommunity.colorscheme.kanagawa-nvim" },
      {
        "rebelot/kanagawa.nvim",
        lazy = false,
      },
      { import = "astrocommunity.colorscheme.github-nvim-theme" }, -- no background support
      {
        "projekt0n/github-nvim-theme",
        lazy = false,
      },
    ```

<!--
  -- Theme testing for visual appeal:
  -- colorscheme = "astrodark",  (default theme, no background support I think)
  -- colorscheme = "catppuccin",   -- light color to pale, lacks contrast
  -- colorscheme = "dayfox",
  colorscheme = "everforest",
  -- colorscheme = "github_light",  -- no background support, otherwise quite nice
  -- colorscheme = "gruvbox",  -- status and tablines inverted - doesnt look good, - requires highlight setting in user config
  -- colorscheme = "gruvbox-baby", -- no background support
  -- colorscheme = "kanagawa",  -- nice
  -- colorscheme = "onigiri",  -- nice
  -- colorscheme = "oxocarbon", -- written in Fennel
  -- colorscheme = "rose-pine", -- light colour very bright
-->

### Configure Lazy plugins

[:globe_with_meridians: Lazy.nvim Plugin specification](https://github.com/folke/lazy.nvim#-plugin-spec){target=\_blank .md-button}


## Config Format and Lint tools

!!! HINT "Disable format on save when tools provide unexpected results"
    `SPC u f` toggles if the respective format tool should run for the current buffer.  `SPC u F` for all buffers of the current kind.

    `init.lua` lsp section can enable or disable format on save for specific file types.

Mason is responsible for installing lint and format tools

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
            args = {
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

