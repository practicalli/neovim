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

++ctrl+"="++ and ++ctrl+"-"++ increase & decrease the font size in Neovide (move the cursor if no immediate effect is seen)


!!! EXAMPLE "Neovide recipe"
    Astro Community provides an [:fontawesome-solid-book-open: neovide recipe](https://docs.astronvim.com/recipes/neovide) with recommended options.

    ```lua title="lua/plugins/community.lua"
    { import = "astrocommunity.recipes.neovide" },
    ```

    This recipe is include in the `lua/community.lua` file from Practicalli Astro configuration, with a font override in `lua/plugins/user-practicalli.lua` to set the preferred font.

    ```lua
      {
        "AstroNvim/astrocore",
        ---@type AstroCoreOpts
        opts = {
          options = {
            -- configure general options: vim.opt.<key>
            opt = {
              guifont = "Fira Code:h16", -- neovide font family & size (height)
            },  
          },
        },
      }  
    ```

![Neovide Gui Screenshot](https://neovide.dev/assets/BasicScreenCap.png){loading=lazy}

