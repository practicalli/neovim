# Troubleshoot

Issues are typically with a syntax error in the configuration or with a specific plugin.

Use a [minimal configuration](#minimal-config) to help reproduce issues for a specific plugin, narrowing down the potential causes of the issue.

The [:checkhealth](#check-health) command provides diagnostics about Neovim, its  APIs, external requirements (command line tools) and plugin documentation.


## Minimal config

A `repro.lua` file can be used to test a specific plugin or configuration with only a known minimal set of plugins.

Use the `-u` option to run Neovim with a given configuration file.

!!! NOTE ""
    ```shell
    nvim -u repro.lua
    ```

??? INFO "Folke Lazy minimal config to reproduce issue"
    Folke/Lazy provides a [minimal init.lua to reproduce an issue](https://github.com/folke/lazy.nvim/wiki/Minimal-%60init.lua%60-to-Reproduce-an-Issue)

    ```lua
    local root = vim.fn.fnamemodify("./.repro", ":p")

    -- set stdpaths to use .repro
    for _, name in ipairs({ "config", "data", "state", "cache" }) do
      vim.env[("XDG_%s_HOME"):format(name:upper())] = root .. "/" .. name
    end

    -- bootstrap lazy
    local lazypath = root .. "/plugins/lazy.nvim"
    if not vim.loop.fs_stat(lazypath) then
      vim.fn.system({
        "git",
        "clone",
        "--filter=blob:none",
        "--single-branch",
        "https://github.com/folke/lazy.nvim.git",
        lazypath,
      })
    end
    vim.opt.runtimepath:prepend(lazypath)

    -- install plugins
    local plugins = {
      -- do not remove the colorscheme!
      "folke/tokyonight.nvim",
      -- add any other pugins here
    }
    require("lazy").setup(plugins, {
      root = root .. "/plugins",
    })

    -- add anything else here
    vim.opt.termguicolors = true
    -- do not remove the colorscheme!
    vim.cmd([[colorscheme tokyonight]])
    ```

??? INFO "Repro for Astrocommunity issues"
    Raising an issue on [Astrocommunity](https://github.com/AstroNvim/astrocommunity) will generate a `repro.lua` config once the issue is created. Add the plugin or config to test

??? EXAMPLE "Repro config for Practicalli Astro 5"
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


## Check Health

`:checkhealth` command provides detailed information of the configuration and supporting tools.

Run the `:checkhealth` command within Neovim, or start Neovim and run `:checkhealth` on startup.

!!! NOTE ""
    ```shell
    nvim +:checkhealth
    ```

## Sections

`:checkhealth` can be used to view specific help sections, e.g. neovim APIs. Each plugin should include its own help section too.


### Lazy plugin manager

Check the health of the Lazy plugin manager.

!!! NOTE ""
    ```shell
    nvim +:checkhealth
    ```

??? "Output of :checkhealth lazy"
    ```shell-session
    ==============================================================================
    lazy:                                           require("lazy.health").check()

    lazy.nvim ~
    - {lazy.nvim} version `11.17.1`
    - OK {git} `version 2.47.2`
    - OK no existing packages found by other package managers
    - OK packer_compiled.lua not found

    luarocks ~
    - checking `luarocks` installation
    - you have some plugins that require `luarocks`:
        * `rest.nvim`
    - OK {luarocks} `/usr/bin/luarocks 3.8.0`
    - OK {lua5.1} `Lua 5.1.5  Copyright (C) 1994-2012 Lua.org, PUC-Rio`
    ```


### Neovim Deprecated APIs

Neovim releases occasionally contain breaking changes as the API evolves.

When upgrading to a new Neovim version, check `vim.deprecated` for Neovim API breaking changes.

Plugin maintainers will also find deprecation notices for future planned releases of Neovim, so they can ensure plugins work as soon as the new release is available.

!!! NOTE ""
    ```shell
    nvim +:checkhealth vim.depricated
    ```

??? EXAMPLE "Output of :checkhealth vim.deprecated"
    ```shell-session
    ==============================================================================
    vim.deprecated:                       require("vim.deprecated.health").check()

     ~
    - WARNING client.request is deprecated. Feature will be removed in Nvim 0.13
      - ADVICE:
        - use client:request instead.
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/lsp/init.lua:39
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/init.lua:129
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/init.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/init.lua:251
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/autocommands.lua:88
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/lsp/init.lua:39
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/util.lua:10
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/lsp/init.lua:39
            /home/practicalli/.local/share/nvim-astro5/lazy/aerial.nvim/lua/aerial/backends/util.lua:10
            vim/_editor.lua:0
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/which-key.nvim/lua/which-key/state.lua:262
            /home/practicalli/.local/share/nvim-astro5/lazy/which-key.nvim/lua/which-key/state.lua:346
            /home/practicalli/.local/share/nvim-astro5/lazy/which-key.nvim/lua/which-key/triggers.lua:44

     ~
    - WARNING client.supports_method is deprecated. Feature will be removed in Nvim 0.13
      - ADVICE:
        - use client:supports_method instead.
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:132
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:210
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:135
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:146
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:210
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:135
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_mappings.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:177
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:210
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:135
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_mappings.lua:111
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:177
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:210
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/client.lua:135
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:132
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:216
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/core/picker.lua:688
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:36
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_mappings.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:177
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:216
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/core/picker.lua:688
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:36
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_mappings.lua:111
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:177
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:216
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/core/picker.lua:688
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:36
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:132
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:211
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:491
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:1023
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:936
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:624
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:130
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:161
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:220
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/async.lua:5
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:146
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:211
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:491
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:1023
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:936
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:624
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:130
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:161
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:220
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/async.lua:5
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_mappings.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:177
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:211
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:491
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:1023
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:936
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:624
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:130
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:161
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:220
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/async.lua:5
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_mappings.lua:111
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:177
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:244
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:255
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/configs.lua:211
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:491
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:1023
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:936
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp.lua:624
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:130
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:161
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/manager.lua:220
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nvim-lspconfig/lua/lspconfig/async.lua:5
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:156

     ~
    - WARNING vim.region is deprecated. Feature will be removed in Nvim 0.13
      - ADVICE:
        - use vim.fn.getregionpos() instead.
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/highlight.lua:53
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/highlight.lua:24
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/engine.lua:190
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/engine.lua:158
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/highlight.lua:53
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/highlight.lua:24
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/engine.lua:190
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/vim-illuminate/lua/illuminate/engine.lua:158
            vim/_editor.lua:0
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/which-key.nvim/lua/which-key/state.lua:262
            /home/practicalli/.local/share/nvim-astro5/lazy/which-key.nvim/lua/which-key/state.lua:346
            /home/practicalli/.local/share/nvim-astro5/lazy/which-key.nvim/lua/which-key/state.lua:115

     ~
    - WARNING vim.str_utfindex is deprecated. Feature will be removed in Nvim 1.0
      - ADVICE:
        - use vim.str_utfindex(s, encoding, index, strict_indexing) instead.
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/diff.lua:158
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/formatting.lua:85
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/formatting.lua:84
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/generators.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/generators.lua:192
            /home/practicalli/.local/share/nvim-astro5/lazy/plenary.nvim/lua/plenary/async/async.lua:25
            /home/practicalli/.local/share/nvim-astro5/lazy/plenary.nvim/lua/plenary/async/async.lua:45
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:742
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/buf.lua:598
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:72
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:161
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/diff.lua:159
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/formatting.lua:85
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/formatting.lua:84
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/generators.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/none-ls.nvim/lua/null-ls/generators.lua:192
            /home/practicalli/.local/share/nvim-astro5/lazy/plenary.nvim/lua/plenary/async/async.lua:25
            /home/practicalli/.local/share/nvim-astro5/lazy/plenary.nvim/lua/plenary/async/async.lua:45
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:742
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/buf.lua:598
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:72
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:161

     ~
    - WARNING vim.validate is deprecated. Feature will be removed in Nvim 1.0
      - ADVICE:
        - use vim.validate(name, value, validator, optional_or_msg) instead.
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/mini.icons/lua/mini/icons.lua:1962
            /home/practicalli/.local/share/nvim-astro5/lazy/mini.icons/lua/mini/icons.lua:192
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:387
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/astroui/lua/astroui/status/utils.lua:155
            /home/practicalli/.local/share/nvim-astro5/lazy/astroui/lua/astroui/status/hl.lua:41
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:355
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:473
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/init.lua:114
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/mini.icons/lua/mini/icons.lua:1965
            /home/practicalli/.local/share/nvim-astro5/lazy/mini.icons/lua/mini/icons.lua:192
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:387
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/astroui/lua/astroui/status/utils.lua:155
            /home/practicalli/.local/share/nvim-astro5/lazy/astroui/lua/astroui/status/hl.lua:41
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:355
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:398
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/statusline.lua:473
            /home/practicalli/.local/share/nvim-astro5/lazy/heirline.nvim/lua/heirline/init.lua:114
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/mason-null-ls.nvim/lua/mason-null-ls/settings.lua:46
            /home/practicalli/.local/share/nvim-astro5/lazy/mason-null-ls.nvim/lua/mason-null-ls/init.lua:82
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/mason-null-ls.lua:3
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/none-ls.lua:25
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:354
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:353
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/handler/event.lua:85
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/astrocore/lua/astrocore/init.lua:105
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:8
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:67
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:293
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:533
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:571
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:8
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:68
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:293
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:533
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:571
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:575
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:53
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:427
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:494
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:61
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:428
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:494
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:8
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:67
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:155
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:461
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:494
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:8
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:68
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:155
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:461
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:494
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_snipmate.lua:497
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:53
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_lua.lua:379
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_lua.lua:446
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:61
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_lua.lua:380
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_lua.lua:446
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_lua.lua:450
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/configs/luasnip.lua:3
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:119
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:8
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:67
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:293
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:533
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:571
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:121
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:8
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/util.lua:68
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:293
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:533
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:571
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:121
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/from_vscode.lua:575
            /home/practicalli/.config/nvim-astro5/lua/plugins/practicalli.lua:121
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:380
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/util.lua:135
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:395
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:362
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:197
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:543
            /home/practicalli/.local/share/nvim-astro5/lazy/lazy.nvim/lua/lazy/core/loader.lua:564
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:44
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/init.lua:37
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/init.lua:182
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:20
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:104
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/filetype.lua:36
            [C]:-1
            vim/shared.lua:0
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/filetype.lua:35
            [C]:-1
            vim/_editor.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:115
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:36
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            vim/_editor.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:115
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/picker/actions.lua:36
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/snippets/luasnip.lua:70
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/provider/list.lua:47
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/provider/init.lua:88
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/async.lua:65
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/tree.lua:89
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/queue.lua:48
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/init.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:20
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/event_emitter.lua:28
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/trigger/init.lua:270
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/trigger/init.lua:122
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:81
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/init.lua:37
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/init.lua:182
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:20
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/config/snippets.lua:45
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:45
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:154
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:249
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:94
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:280
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:100
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:76
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/init.lua:146
            vim/_editor.lua:0
            vim/_editor.lua:0
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:742
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/buf.lua:598
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:72
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:161
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/autocmd.lua:376
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:172
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:171
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:251
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:94
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:280
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:100
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:76
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/init.lua:146
            vim/_editor.lua:0
            vim/_editor.lua:0
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/client.lua:742
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/lsp/buf.lua:598
            /home/practicalli/.local/share/nvim-astro5/lazy/AstroNvim/lua/astronvim/plugins/_astrolsp_autocmds.lua:72
            /home/practicalli/.local/share/nvim-astro5/lazy/astrolsp/lua/astrolsp/init.lua:161
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:383
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:555
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:390
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:555
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:396
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:555
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:455
            /home/practicalli/.local/share/nvim-astro5/lazy/mason.nvim/lua/mason-core/ui/display.lua:555
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/util/init.lua:93
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/win.lua:798
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/notifier.lua:706
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/notifier.lua:352
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/notifier.lua:332
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/snacks.nvim/lua/snacks/notifier.lua:331
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:154
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:249
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:284
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:100
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:76
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/lsp/progress.lua:57
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/lsp/progress.lua:46
            vim/_editor.lua:0
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/autocmd.lua:376
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:172
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:171
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:251
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:284
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:100
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/backend/mini.lua:76
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/lsp/progress.lua:57
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/lsp/progress.lua:46
            vim/_editor.lua:0
            vim/_editor.lua:0
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:154
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:249
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:94
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:280
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:88
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:27
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:138
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/autocmd.lua:376
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:172
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:171
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:251
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:94
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:280
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:88
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:27
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:138
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/window/init.lua:113
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/windows/menu.lua:95
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/windows/menu.lua:61
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:70
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/event_emitter.lua:28
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/list.lua:96
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:53
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/window/init.lua:132
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/windows/menu.lua:95
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/windows/menu.lua:61
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:70
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/event_emitter.lua:28
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/list.lua:96
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:53
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:154
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:249
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:284
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:88
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:27
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:138
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/utils/autocmd.lua:376
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:172
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:171
            /home/practicalli/.local/share/nvim-astro5/lazy/nui.nvim/lua/nui/popup/init.lua:251
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:107
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/nui.lua:284
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:163
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/view/init.lua:170
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/message/router.lua:214
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/util/call.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:88
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:27
            /home/practicalli/.local/share/nvim-astro5/lazy/noice.nvim/lua/noice/ui/init.lua:138
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            vim/_editor.lua:0
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/health.lua:379
            nvim>:1
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
            [C]:-1
            /tmp/.mount_nvimEOCGje/usr/share/nvim/runtime/lua/vim/health.lua:386
            nvim>:1
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/loaders/init.lua:136
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/plugin/luasnip.lua:87
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/snippets/luasnip.lua:70
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/provider/list.lua:47
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/provider/init.lua:88
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/async.lua:65
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/tree.lua:89
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/queue.lua:48
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/init.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:20
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/event_emitter.lua:28
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/trigger/init.lua:270
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/trigger/init.lua:63
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:53
        - stack traceback:
            /home/practicalli/.local/share/nvim-astro5/lazy/LuaSnip/lua/luasnip/util/util.lua:350
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/snippets/luasnip.lua:70
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/provider/list.lua:47
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/provider/init.lua:88
            [C]:-1
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/async.lua:65
            vim/shared.lua:0
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/tree.lua:89
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/queue.lua:48
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/sources/lib/init.lua:149
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/init.lua:20
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/event_emitter.lua:28
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/trigger/init.lua:270
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/completion/trigger/init.lua:56
            /home/practicalli/.local/share/nvim-astro5/lazy/blink.cmp/lua/blink/cmp/lib/buffer_events.lua:53

    ```

### LSP Health

!!! NOTE ""
    ```shell
    nvim +:checkhealth vim.lsp
    ```

??? EXAMPLE "Output of Checkhealth Vim LSP"
    ```shell-session
    ==============================================================================
    vim.treesitter:                       require("vim.treesitter.health").check()

    Treesitter features ~
    - Treesitter ABI support: min 13, max 15
    - WASM parser support: false

    Treesitter parsers ~
    - OK Parser: bash                 ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/bash.so
    - OK Parser: c                    ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/c.so
    - OK Parser: c                    ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/c.so
    - OK Parser: clojure              ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/clojure.so
    - OK Parser: html                 ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/html.so
    - OK Parser: http                 ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/http.so
    - OK Parser: json                 ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/json.so
    - OK Parser: jsonc                ABI: 13, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/jsonc.so
    - OK Parser: lua                  ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/lua.so
    - OK Parser: lua                  ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/lua.so
    - OK Parser: luap                 ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/luap.so
    - OK Parser: markdown             ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/markdown.so
    - OK Parser: markdown             ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/markdown.so
    - OK Parser: markdown_inline      ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/markdown_inline.so
    - OK Parser: markdown_inline      ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/markdown_inline.so
    - OK Parser: python               ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/python.so
    - OK Parser: query                ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/query.so
    - OK Parser: query                ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/query.so
    - OK Parser: regex                ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/regex.so
    - OK Parser: vim                  ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/vim.so
    - OK Parser: vim                  ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/vim.so
    - OK Parser: vimdoc               ABI: 14, path: /home/practicalli/.local/share/nvim-astro5/lazy/nvim-treesitter/parser/vimdoc.so
    - OK Parser: vimdoc               ABI: 14, path: /tmp/.mount_nvimEOCGje/usr/lib/nvim/parser/vimdoc.so
    ```



## Checkhealth examples

`:checkhealth snacks`

```text
==============================================================================
snacks: require("snacks.health").check()

    Snacks ~
    - OK setup called

    Snacks.bigfile ~
    - WARNING setup {disabled}

    Snacks.dashboard ~
    - OK setup {enabled}
    - OK setup ran
    - WARNING dashboard did not open: `argc(-1) > 0`

    Snacks.explorer ~
    - WARNING setup {disabled}

    Snacks.image ~
    - OK setup {enabled}
    - OK 'kitty' `kitty 0.39.1 created by Kovid Goyal`
    - OK 'magick' `Version: ImageMagick 7.1.1-43 Q16 x86_64 22550 https://imagemagick.org`
    - OK 'convert' `Version: ImageMagick 7.1.1-43 Q16 x86_64 22550 https://imagemagick.org`
    - OK `kitty` detected and supported
    - OK `kitty` supports unicode placeholders
    - OK Inline images are available
    - OK Terminal Dimensions:
      - {size}: `1755` x `1647` pixels
      - {scale}: `1.63`
      - {cell}: `13` x `27` pixels
    - OK Available Treesitter languages:
        `markdown_inline`, `markdown`
    - WARNING Missing Treesitter languages:
        `css`, `html`, `javascript`, `latex`, `norg`, `scss`, `svelte`, `tsx`, `typst`, `vue`
    - WARNING Image rendering in docs with missing treesitter parsers won't work
    - OK 'gs' `10.05.0`
    - OK PDF files are supported
    - ERROR None of the tools found: 'tectonic', 'pdflatex'
    - WARNING `tectonic` or `pdflatex` is required to render LaTeX math expressions
    - ERROR Tool not found: 'mmdc'
    - WARNING `mmdc` is required to render Mermaid diagrams
    - OK your terminal supports the kitty graphics protocol

    Snacks.input ~
    - OK setup {enabled}
    - OK `vim.ui.input` is set to `Snacks.input`

    Snacks.lazygit ~
    - OK {lazygit} installed

    Snacks.notifier ~
    - OK setup {enabled}
    - OK is ready

    Snacks.picker ~
    - OK setup {enabled}
    - OK `vim.ui.select` is set to `Snacks.picker.select`
    - OK Available Treesitter languages:
        `regex`
    - OK 'git' `git version 2.47.2`
    - OK 'rg' `ripgrep 14.1.1`
    - OK `Snacks.picker.grep()` is available
    - OK 'fdfind' `fdfind 10.2.0`
    - OK `Snacks.picker.files()` is available
    - OK `Snacks.picker.explorer()` is available
    - OK `SQLite3` is available

    Snacks.quickfile ~
    - WARNING setup {disabled}

    Snacks.scope ~
    - OK setup {enabled}

    Snacks.scroll ~
    - WARNING setup {disabled}

    Snacks.statuscolumn ~
    - WARNING setup {disabled}

    Snacks.terminal ~
    - OK shell configured
      - `vim.o.shell`: /usr/bin/zsh
      - `parsed`: { "/usr/bin/zsh" }

    Snacks.toggle ~
    - OK {which-key} is installed

    Snacks.words ~
    - WARNING setup {disabled}
```
