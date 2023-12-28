# Neovide GUI



![Neovide Gui Screenshot](https://neovide.dev/assets/neovide-128x128.png){align=right loading=lazy style="height:150px"}

Neovide provides a GUI for Neovim and supports the use of AstroNvim community configuration.

[:globe_with_meridians: Neovide features](https://neovide.dev/features.html){target=_blank}

## Install Neovide

[:globe_with_meridians: Download from Neovide.dev website](https://neovide.dev/)

=== "Debian"
    [Download neovide.AppImage](https://github.com/neovide/neovide/releases/latest/download/neovide.AppImage)

    Move the `neovide.AppImage` to the execution path, e.g. `$HOME/.local/bin`

    Create the `$HOME/.local/bin/neovide` symbolic link pointing to the neovide.AppImage

    !!! NOTE ""
        ```shell
        ln -s $HOME/.local/bin/neovide.AppImage $HOME/.local/bin/neovide
        ```

=== "MacOSX"

    [Download the MacOSX dmg.zip file](https://github.com/neovide/neovide/releases/latest/download/neovide.dmg.zip)

    Extract the .zip file 

    Run the extracted dmg file and use the install wizard to copy Neovide to the Applications directory.

    Create symbolic link from Neovide install to `~/.local/bin` 

    ```bash
    ln -s /Applications/neovide.app/Contents/MacOS/neovide ~/.local/bin/neovide
    ```

    Add alias to use neovide with astronvim configuration to `.bashrc` , `.zshrc` or shared `shell-aliases` file

    ```shell
    alias neovide="NVIM_APPNAME=astronvim neovide"
    ```


## Neovide with NVIM_APPNAME

`NVIM_APPNAME` sets the configuration used when starting Neovim.

Use a shell alias to run Neovide with a specific configuration

```shell
# Neovide alias with AstroNvim configuration
alias neovide="NVIM_APPNAME=astronvim neovide"
```


## Set Neovide Font

The `guifont` Neovim option is used to set a font family and size specifically for a GUI appliction, i.e. Neovide.  It is not used by Neovim itself.


!!! EXAMPLE "Neovide font family and size"
    ```lua
    guifont = "Fira Code:h16"
    ```


!!! EXAMPLE "AstroNvim Neovide font family and size"
    [:fontawesome-solid-book-open: Practicalli AstroNvim Config](/neovim/configuration/astronvim/#clone-astronvim-user-config) includes the `guifont` option in the `options.lua` file.

    ```lua title="options.lua"
    return {
      opt = {
        -- set to true or false etc.
        relativenumber = true, -- sets vim.opt.relativenumber
        number = true,         -- sets vim.opt.number
        spell = false,         -- sets vim.opt.spell
        signcolumn = "auto",   -- sets vim.opt.signcolumn to auto
        wrap = true,           -- sets vim.opt.wrap
        -- showtabline = 0,    -- sets vim.opt.showtabline - zero hides tabs
        timeoutlen = 420,
        -- neovide font family & size
        guifont = "Fira Code:h16",
      },
    }
    ```

![Neovide Gui Screenshot](https://neovide.dev/assets/BasicScreenCap.png){loading=lazy}

