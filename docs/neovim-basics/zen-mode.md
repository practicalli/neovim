# Focus Modes

Focus on the code or text being created, without distractions

`zZ` toggles Zen mode

`SPC z a` ataraxis focus mode

`SPC z f` focus current buffer

`SPC z n` narrow to current buffer

`SPC z n` remove status bar and window decorations

`v SPC z n` narrow to selection


## Zen Mode

[Zen Mode](https://github.com/folke/zen-mode.nvim) distraction-free coding for Neovim

Available via the Astrocommunity repository.

!!! EXAMPLE "Zen Mode configuration for AstroNvim"
    ```lua title=".config/astronvim-config/plugins/community.lua"
      { import = "astrocommunity.editing-support.zen-mode-nvim" },
      {
        "folke/zen-mode.nvim",
        opts = {
          -- override default configuration
          -- https://github.com/folke/zen-mode.nvim#%EF%B8%8F-configuration
          plugins = {
            options = {
              enabled = true,
            },
            kitty = {
              enabled = true,
              font = "+4", -- font size increment
            },
          },
        },
      },
    ```

[kitty configuration](#kitty-configuration) enables Zen Mode to resize kitty fonts.


## True Zen

[true-zen.nvim](https://github.com/Pocco81/true-zen.nvim) clean and elegant distraction-free writing for NeoVim

!!! EXAMPLE "True Zen Mode configuration for AstroNvim"
    ```lua
      {
        "Pocco81/true-zen.nvim",
        lazy = false,
        opts = {
          integrations = {
            kitty = {
              -- increment font size in Kitty.
              enabled = true,
              font = "+4",
            },
          },
        },
      },
    ```

See [kitty configuration](#kitty-configuration) to enable Zen Mode to resize kitty fonts.


## Kitty configuration

Add `allow_remote_control socket-only` and `listen_on unix:/tmp/kitty` to the kitty config

!!! EXAMPLE "Kitty support for Zen Mode"
    ```config title=".config/kitty/kitty.config"
    # ---------------------------------------------------------
    #  Neovim zen-mode-nvim
    #  - change the font size on kitty when in zen mode
    allow_remote_control socket-only
    listen_on unix:/tmp/kitty
    # ---------------------------------------------------------
    ```
