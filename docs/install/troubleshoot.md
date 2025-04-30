# Troubleshoot

`:checkhealth` command provides detailed information of the configuration and supporting tools.

Run the `:checkhealth` command within Neovim, or start Neovim and run `:checkhealth` on startup.

!!! NOTE ""
    ```shell
    nvim +:checkhealth
    ```


## Sections

`:checkhealth` can be used to view specific sections


For Neovim API breaking changes

!!! NOTE ""
    ```shell
    nvim +:checkhealth vim
    ```


## Minimal Repro config

A `repro.lua` file can be used to test a specific plugin or configuration with only a known minimal set of plugins.

??? INFO "Repro for Astrocommunity issues"
    Raising an issue on [Astrocommunity](https://github.com/AstroNvim/astrocommunity) will generate a `repro.lua` config once the issue is created.  Add the plugin or config to test


!!! EXAMPLE "Repro config for Practicalli Astro 5"
    ```lua
    -- save as repro.lua
    -- run with nvim -u repro.lua
    -- DO NOT change the paths
    local root = vim.fn.fnamemodify("./.repro", ":p")

    -- set stdpaths to use .repro
    for _, name in ipairs { "config", "data", "state", "runtime", "cache" } do
      vim.env[("XDG_%s_HOME"):format(name:upper())] = root .. "/" .. name
    end

    -- bootstrap lazy
    local lazypath = root .. "/plugins/lazy.nvim"
    if not vim.loop.fs_stat(lazypath) then
      -- stylua: ignore
      vim.fn.system({ "git", "clone", "--filter=blob:none", "https://github.com/folke/lazy.nvim.git", "--branch=stable", lazypath })
    end
    vim.opt.rtp:prepend(vim.env.LAZY or lazypath)

    -- install plugins
    local plugins = {
      { "AstroNvim/AstroNvim", import = "astronvim.plugins" },
      { "AstroNvim/astrocommunity" },

      -- add any other plugins/customizations here
    }
    require("lazy").setup(plugins, {
      root = root .. "/plugins",
    })

    -- add anything else here (autocommands, vim.filetype, etc.)
    ```
