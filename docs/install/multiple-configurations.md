## Multiple Configurations

Many Neovim configurations can be installed in `$HOME/.config/` using unique directory names, e.g. [AstroNvim](astronvim/), cajus, lazyvim, kickstart.

Set `NVIM_APPNAME` to a configuration directory name (relative to $HOME/.config/`) to run Neovim with that specific config.

!!! NOTE "Run AstroNvim config in `$HOME/.config/astronvim/`"
    ```shell
    NVIM_APPNAME=astronvim nvim
    ```

The configuration directory name is used to save local `share`, `state` and `cache` files for that specific configuration.

??? INFO "Community Configuration Projects"

    * [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim) a highly documented starter configuration to effectively build your own
    * [LazyVim](https://www.lazyvim.org/) lazy & mason configuration
    * [Magit Kit](https://github.com/Olical/magic-kit) fennel configuration from the author of Conjure
    * [cajus-nvim](https://github.com/rafaeldelboni/cajus-nvim) inspiration for practicalli/neovim-config-redux


## Configure shell alias

Create a Shell alias for each configuration that will be used, to avoid setting the `NVIM_APPNAME` variable each time.

Add alias to `.bashrc` for Bash shell or `.zshrc` for Zsh

!!! EXAMPLE "Define Shell Aliases to run each configuration"
    ```shell
    alias astro="NVIM_APPNAME=nvim-astro nvim"
    alias lazy="NVIM_APPNAME=nvim-lazyvim nvim"
    alias cajus="NVIM_APPNAME=nvim-cajus nvim"
    ```


### shell-aliases for bash and zsh

Create a `.config/shell-aliases` file containing all shell aliases when often switching between different shells, avoiding the need to define aliases twice

Source the `.config/shell-aliases` file from within `.bashrc` or `.zshrc`

=== "Zsh"
    ```shell title=".zshrc"
    # Shell Aliases
    [[ ! -f ~/.config/shell-aliases ]] || source ~/.config/shell-aliases
    ```

=== "Bash"
    ```shell title=".bashrc"
    # Shell Aliases
    if [ -f ~/.config/shell-aliases ]; then
        . ~/.config/shell-aliases
    fi
    ```

## Neovim config selector

Create a shell function to popup a menu with the list of available Neovim configurations, defined in `~/.config` where the configuration directories are prefixed with `nvim-`, e.g. `~/.config/nvim-astro/`

![Neovim Config Fuzy Selector](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-config-selector-fuzzy-find-config-list-dark.png?raw=true){loading=lazy}

!!! EXAMPLE "Neovim Config Fuzzy Finder"

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
    Add the Neovim config directory names from `~/.config/`
    ```shell title=".local/bin/nvim-selector"
     nvim-selector() {
      select config in nvim-astro nvim-astronvim-template nvim-lazyvim nvim-kickstart
      do NVIM_APPNAME=nvim-$config nvim $@; break; done
    }
    ```
