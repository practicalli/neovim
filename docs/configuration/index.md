# Neovim Configuration

Practicalli Neovim covers the following configurations.

- [AstroNvim](astronvim.md) - thoughtful configuration, supports Neovim 0.9 onward, polished UI, many community extensions
- [Practicalli Neovim Config Redux](practicalli.md) - mnemonic key bindings, packer, telescope selector, written in Fennel


## Multiple Configurations

Install multiple configurations, e.g. [AstroNvim](astronvim.md), lazyvim, Nvchad, etc. in the `$HOME/.config` directory using unique directory names.

Set `NVIM_APPNAME` to specific the configuration to use when running nvim.

!!! NOTE ""
    ```shell
    NVIM_APPNAME=astronvim nvim
    ```

`NVIM_APPNAME` variable should be set to the directory name containing the configuration, relative to the `.config` directory.

The configuration directory name is used to hold `share`, `state` and `cache` files for that specific configuration.

Create shell aliases for each configuration. Optionalliy, define a terminal UI selection to choose a configuration.

=== "Shell Aliases"
    Create a Shell alias for each configuration that will be used, to avoid setting the `NVIM_APPNAME` variable each time.
    !!! EXAMPLE "Define Shell Aliases to run each configuration"
        ```shell
        alias astro="NVIM_APPNAME=astronvim nvim"
        alias lazyvim="NVIM_APPNAME=lazyvim nvim"
        alias practicalli-redux="NVIM_APPNAME=neovim-config-redux nvim"
        ```

=== "Terminal UI Selector"
    Create an nvim configuration selector script, with items listing the directory name of each configuration
    !!! EXAMPLE "Z Shell nvim-selector script"
        ```zsh title=".local/bin/nvim-selector"
        function nvim-selector() {
          items=("astronvim" "neovim-config-redux" "lazyvim")
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
