# Multiple Configurations

Many different Neovim configurations can be used at the same time, by instaling each config in `$HOME/.config/` using unique directory names

??? INFO "Community Configuration Projects"
    - [Kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim) a highly documented starter to effectively build your own configuration
    - [LazyVim](https://www.lazyvim.org/) lazy & mason configuration
    - [Magit Kit](https://github.com/Olical/magic-kit) fennel configuration from the author of Conjure
    - [cajus-nfnl](https://github.com/rafaeldelboni/cajus-nfnl) fennel-based config
    - [AstroNvim](https://astronvim.com/) rich Neovim experience


??? TIP "Always have a working config"
    Create a separate configuration when making major changes to your configuration or starting a new configuration from scratch.


## NVIM_APPNAME environment variable

Set `NVIM_APPNAME` to a configuration directory name (relative to `$HOME/.config/`) to run Neovim with that specific config.

!!! NOTE "Run AstroNvim config in `$HOME/.config/astronvim/`"
    ```shell
    NVIM_APPNAME=astronvim nvim
    ```

The configuration directory name is used to save local `share`, `state` and `cache` files for that specific configuration.


## Configure shell alias

Create a Shell alias for each configuration that will be used, to avoid setting the `NVIM_APPNAME` variable each time.

Add alias to `.bashrc` for Bash shell, `.zshrc` for Zsh or use a common [shell-aliases]() file.

!!! EXAMPLE "Define Shell Aliases to run each configuration"
    ```shell
    alias astro="NVIM_APPNAME=nvim-astro5 nvim"
    alias lazyvim="NVIM_APPNAME=nvim-lazyvim nvim"
    alias cajus="NVIM_APPNAME=nvim-cajus nvim"
    ```


### shell-aliases

Create a `.config/shell-aliases` file containing all shell aliases which can be used with any shell.

A common shell-aliases file is very useful when switching between different shells, avoiding the need to define aliases twice.

Source the `.config/shell-aliases` file from within `.bashrc` or `.zshrc`

=== "Zsh"

    !!! NOTE ""
        Load (source) aliases
        ```shell title=".zshrc"
        # Shell Aliases
        [[ ! -f ~/.config/shell-aliases ]] || source ~/.config/shell-aliases
        ```

=== "Bash"

    !!! NOTE ""
        Load (source) aliases
        ```shell title=".bashrc"
        # Shell Aliases
        if [ -f ~/.config/shell-aliases ]; then
            . ~/.config/shell-aliases
        fi
        ```

## Neovim config selector

Create a shell function to popup a menu with the list of available Neovim configurations, defined in `~/.config` where the configuration directories are prefixed with `nvim-`, e.g. `~/.config/nvim-astro5/`

![Neovim Config Fuzy Selector](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-config-selector-fuzzy-find-config-list-dark.png?raw=true){loading=lazy}

!!! EXAMPLE "Neovim Config Fuzzy Finder"
    List every neovim configuration in `$HOME/.config`, any directory starting with `nvim-` name.
    ```shell title=".local/bin/nvim-fuzy-find"
    nvim-fuzy-find() {
      # All config paths are prefixed with ~/.config/nvim-
      local config=$(fdfind --max-depth 1 --glob 'nvim-*' ~/.config | fzf --prompt="Neovim Configs > " --height=15% --layout=reverse --border --exit-0)

      [[ -z $config ]] && echo "No config selected, Neovim not starting" && return

      # Open Neovim with selected config
      NVIM_APPNAME=$(basename $config) nvim $@
    }
    ```

??? EXAMPLE "Neovim Config simple Selector"
    Add specific Neovim config directory names from `~/.config/`
    ```shell title=".local/bin/nvim-selector"
     nvim-selector() {
      select config in nvim-astro5 nvim-astronvim5-template nvim-lazyvim nvim-kickstart
      do NVIM_APPNAME=nvim-$config nvim $@; break; done
    }
    ```
