# Customise Configuration

Customise the Practicalli Astro5 configuration without needing to break from future pull requests (or manage merging)

??? INFO "Practicalli Astro 5 file structure"
    ```shell
    ├── after
    │   └── ftplugin
    │       └── clojure.lua       # Config loaded after clojure filetype buffer opened
    ├── CHANGELOG.md
    ├── ftdetect
    │   └── bb.vim                # Set Babashka *.bb files to Clojure filetype
    ├── init.lua
    ├── lazy-lock.json            # Optional: when identical plugin version install required
    ├── lua
    │   ├── community.lua         # Astrocommunity plugin specs
    │   ├── lazy_setup.lua        # Setup Lazy plugin manager, default plugins
    │   └── plugins
    │       ├── practicalli.lua   # Preferences of the Practicalli team
    │       ├── termux.lua        # Use local LSP servers for Neovim on Termux (Android)
    ├── neovim.yml                # Linter config
    ├── README.md
    ├── selene.toml               # Selene idiomatic lua code config
    ├── snippets                  # Snippets (show in completion)
        ├── clojure.json
        ├── global.json
        ├── lua.json
        ├── markdown.json
        └── package.json
    ```


## Disable Practicalli preferences

`lua/plugins/practicalli.lua` contains neovim options, plugins and mappings that the Practicalli team prefer, but may not be suitable to everyones workflow.

Set the `PRACTICALLI_ASTRO` environment variable to `false` to prevent that specific file from being loaded.

!!! NOTE ""
    ```shell
    export PRACTICALLI_ASTRO=false
    ```


## Personal Config

Create your own version of `lua/plugins/practicalli.lua` to override a few configurations or as a complete replacement.

!!! INFO "Practicalli will never add a user.lua file to the config"
    Updates to Practicalli Astro5 will not cause Git merge conflicts for a personal user.lua file.

Use the `lua/plugins/practicalli.lua` file as an example.

Ensure the file returns a table (map of key value pairs).

!!! EXAMPLE "Return a table in each lua file"
    ```lua
    return {
      -- configuration within tables
    }
    ```

Local variables can be defined before the return statement and those variables used throughout the config in the current file.

!!! EXAMPLE "Return a table in each lua file"
    ```lua
    local user_practicalli = vim.env.PRACTICALLI_ASTRO

    return {
      -- configuration within tables
    }
    ```

### Snacks configuration

[folke/snacks](https://github.com/folke/snacks.nvim) plugins are included in Practicalli Astro 5 and provide an excellent user experience.

Add the Snack plugin to configuration one or more of the plugins it contains.

Each plugin is defined within its own key, e.g. `dashboard` for the startup dashbord screen, `indent` for indentation guide lines, etc.

!!! EXAMPLE "Folke Snacks overrides"
    ```lua
    ---@type LazySpec
    return {
      -- Snacks Customisation
      {
        "folke/snacks.nvim",
        opts = {
          dashboard = {
            preset = {
              -- customize the dashboard header
              header = table.concat({
                " ██████╗ ██████╗  █████╗  ██████╗████████╗██╗ ██████╗ █████╗ ██╗     ██╗     ██╗",
                " ██╔══██╗██╔══██╗██╔══██╗██╔════╝╚══██╔══╝██║██╔════╝██╔══██╗██║     ██║     ██║",
                " ██████╔╝██████╔╝███████║██║        ██║   ██║██║     ███████║██║     ██║     ██║",
                " ██╔═══╝ ██╔══██╗██╔══██║██║        ██║   ██║██║     ██╔══██║██║     ██║     ██║",
                " ██║     ██║  ██║██║  ██║╚██████╗   ██║   ██║╚██████╗██║  ██║███████╗███████╗██║",
                " ╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝   ╚═╝   ╚═╝ ╚═════╝╚═╝  ╚═╝╚══════╝╚══════╝╚═╝",
              }, "\n"),
            },
          },

          -- indent guides - disable by default
          indent = { enabled = false },

          -- log level: TRACE DEBUG ERROR WARN INFO  OFF
          notifier = { level = vim.log.levels.WARN },
        },
      },
    }
    ```


### Set Neovim options and key mappings

- Set `vim.opt` options  (`vim/o`) and global options
- Define additional key maps or disable existing key maps

Key maps are defined within the `mappings` key and the specific mode they are enabled (i.e. normal, terminal, visual)

!!! EXAMPLE "Neovim options and key mappings"
    ```lua
    -- ---------------------------------------------------------
    -- Example user configuration
    --
    -- Add over-ride Nvim options, plugins and key mappings
    -- `lua/plugins/practicallli.lua` has more examples
    -- ---------------------------------------------------------

    if true then return {} end -- WARN: REMOVE THIS LINE TO ACTIVATE THIS FILE

    return {
      "AstroNvim/astrocore",
      ---@type AstroCoreOpts
      opts = {
        options = {
          -- configure general options: vim.opt.<key>
          opt = {
            scrolloff = 10, -- line offset when scrolling
          },
          g = {}, -- configure global vim variables: vim.g
        },
        mappings = {
          n = { -- normal mode key bindings
            -- setting a mapping to false will disable it
            -- ["<esc>"] = false,

            -- Toggle last open buffer
            ["<Leader><tab>"] = { "<cmd>b#<cr>", desc = "Previous tab" },

            -- navigate buffer tabs
            ["]b"] = { function() require("astrocore.buffer").nav(vim.v.count1) end, desc = "Next buffer" },
            ["[b"] = { function() require("astrocore.buffer").nav(-vim.v.count1) end, desc = "Previous buffer" },

            -- snacks file explorer
            ["<Leader>E"] = { "<cmd>lua Snacks.picker.explorer()<cr>", desc = "Snacks Explorer" },

            -- Save prompting for file name
            ["<Leader>W"] = { ":write ", desc = "Save as file" },
          },
          t = {}, -- terminal mode key bindings
          v = {}, -- visual mode key bindings
        },
      },
    }
    ```


### Add plugin and configuration

Add a plugin spec and configuration to include a new plugin.

Plugin configuration in a user config will override plugins included via Astrocommunity, `lua/plugins/community.lua` file.

!!! EXAMPLE "Plugins and Plugin options"
    ```lua
    ---@type LazySpec
    return {
      {
        "folke/which-key.nvim",
        opts = {
          ---@type false | "classic" | "modern" | "helix"
          preset = "helix",
        },
      },
      -- Colorscheme (Theme)
      {
        "AstroNvim/astroui",
        ---@type AstroUIOpts
        opts = {
          colorscheme = "catppuccin-mocha",
        },
      },
      -- ------------------------------------------
      -- Editor tools

      -- Alternative to Esc key using `fd` key mapping
      {
        "max397574/better-escape.nvim",
        event = "InsertCharPre",
        opts = {
          timeout = vim.o.timeoutlen,
          default_mappings = false,
          mappings = {
            i = { f = { d = "<Esc>" } },
            c = { f = { d = "<Esc>" } },
            t = { f = { d = "<Esc>" } },
            v = { f = { d = "<Esc>" } },
            s = { f = { d = "<Esc>" } },
          },
        },
      },
      -- Trim trailing blank space and blank lines
      {
        "cappyzawa/trim.nvim",
        event = "User AstroFile",
        opts = {},
      },
      -- Custom snippets (vscode format)
      {
        "L3MON4D3/LuaSnip",
        config = function(plugin, opts)
          -- include default astronvim config that calls the setup call
          require "astronvim.plugins.configs.luasnip"(plugin, opts)
          -- load snippets paths
          require("luasnip.loaders.from_vscode").lazy_load {
            paths = { vim.fn.stdpath "config" .. "/snippets" },
          }
        end,
      },
      -- Switch between src and test file
      {
        "rgroli/other.nvim",
        ft = { "clojure" },
        main = "other-nvim",
        opts = {
          mappings = { "clojure" },
        },
      },
    }
    ```


### Set Neovim options and key mappings

- Set `vim.opt` options  (`vim/o`) and global options
- Define additional key maps or disable existing key maps

Key maps are defined within the `mappings` key and the specific mode they are enabled (i.e. normal, terminal, visual)

!!! EXAMPLE "Neovim options and key mappings"
    ```lua
    -- ---------------------------------------------------------
    -- Example user configuration
    --
    -- Add over-ride Nvim options, plugins and key mappings
    -- `lua/plugins/practicallli.lua` has more examples
    -- ---------------------------------------------------------

    if true then return {} end -- WARN: REMOVE THIS LINE TO ACTIVATE THIS FILE

    return {
      "AstroNvim/astrocore",
      ---@type AstroCoreOpts
      opts = {
        options = {
          -- configure general options: vim.opt.<key>
          opt = {
            scrolloff = 10, -- line offset when scrolling
          },
          g = {}, -- configure global vim variables: vim.g
        },
        mappings = {
          n = { -- normal mode key bindings
            -- setting a mapping to false will disable it
            -- ["<esc>"] = false,

            -- Toggle last open buffer
            ["<Leader><tab>"] = { "<cmd>b#<cr>", desc = "Previous tab" },

            -- navigate buffer tabs
            ["]b"] = { function() require("astrocore.buffer").nav(vim.v.count1) end, desc = "Next buffer" },
            ["[b"] = { function() require("astrocore.buffer").nav(-vim.v.count1) end, desc = "Previous buffer" },

            -- snacks file explorer
            ["<Leader>E"] = { "<cmd>lua Snacks.picker.explorer()<cr>", desc = "Snacks Explorer" },

            -- Save prompting for file name
            ["<Leader>W"] = { ":write ", desc = "Save as file" },
          },
          t = {}, -- terminal mode key bindings
          v = {}, -- visual mode key bindings
        },
      },
    }
    ```
