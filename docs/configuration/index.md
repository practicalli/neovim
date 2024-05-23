# Neovim Configuration

Practicalli Neovim is based on [AstroNvim](astronvim/), a thoughtful configuration that supports the latest Neovim stable releases, provides a polished UI and many community extensions.

Practicalli AstroNvim User Config provides a complete Clojure config on top of AstroNvim.

[Install Practicalli AstroNvim Config](astronvim/index.md){.md-button} 


> NOTE: [Practicalli Neovim Config Redux](practicalli/) was a learning experiment that provided mnemonic key bindings, packer, telescope selector, written in Fennel.  This project has now been archived in favour of AstroNvim


## Multiple Configurations

Many Neovim configurations can be installed in `$HOME/.config/` using unique directory names, e.g. [AstroNvim](astronvim/), lazyvim, Nvchad, practicalli. 

Set `NVIM_APPNAME` to a configuration directory name (relative to $HOME/.config/`) to run Neovim with that specific config.

!!! NOTE "Run AstroNvim config in `$HOME/.config/astronvim/`"
    ```shell
    NVIM_APPNAME=astronvim nvim
    ```

The configuration directory name is used to save local `share`, `state` and `cache` files for that specific configuration.


## Configure shell alias

Create a Shell alias for each configuration that will be used, to avoid setting the `NVIM_APPNAME` variable each time.

Add alias to `.bashrc` for Bash shell or `.zshrc` for Zsh

!!! EXAMPLE "Define Shell Aliases to run each configuration"
    ```shell
    alias astro="NVIM_APPNAME=astronvim nvim"
    alias lazy="NVIM_APPNAME=lazyvim nvim"
    alias practicalli="NVIM_APPNAME=neovim-config nvim"
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

## Zsh Terminal config selector

Optionalliy define a terminal UI selection to choose a configuration if using zsh.

!!! EXAMPLE "Z Shell nvim-selector script"
    ```zsh title=".local/bin/nvim-selector"
    function nvim-selector() {
      items=("astronvim" "practicalli" "lazyvim")
      config=$(printf "%s\n" "${items[@]}" | fzf --prompt=" Neovim Config  " --height=~50% --layout=reverse --border --exit-0)
      if [[ -z $config ]]; then
        echo "Nothing selected"
        return 0
      elif [[ $config == "default" ]]; then
        config=""
      fi
      NVIM_APPNAME=$config nvim $@
    }
    ```
