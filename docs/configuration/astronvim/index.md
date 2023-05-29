# AstroNvim

[:globe_with_meridians: AstroNvim](https://astronvim.com/) is a community configuration with an engaging UI, using Lazy for plugin management (Neovim packages) and Mason for package management (LSP, DAP, format and lint tools)

[:fontawesome-brands-github: Practicalli AstroNvim Config](https://github.com/practicalli/astronvim-config) is a user configuration that extends AstroNvim and imports packages from the [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/user_example).


## Prerequisits

- [Nerd Fonts](https://www.nerdfonts.com/) version 3 - download a full font or only the symbols
- fzf fuzzy finder (ubuntu archive)
- gtu (Ubuntu package archive)
- btm from [GitHub repository releases](https://github.com/ClementTsang/bottom/releases/)

??? INFO "Kitty Terminal with Nerd Fonts"
    [:globe_with_meridians: Kitty Terminal - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/command-line/kitty-terminal/) provides examples of using Nerd Fonts or Nerd Font symbols with the Kitty terminal.

## Clone AstroNvim

Clone AstroNvim repository to `$HOME/.config/astronvim/`

!!! NOTE ""
    ```shell
    git clone --depth 1 https://github.com/AstroNvim/AstroNvim ~/.config/astronvim
    ```

> `$HOME/.config/nvim` can be used instead if only ever using one configuration for Neovim.


## Clone AstroNvim user config

AstroNvim provides a [:fontawesome-brands-github: template repository](https://github.com/AstroNvim/user_example) to create a user configuration. The template includes [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/user_example) configuration to make it easier to extend the feature of AstroNvim.

[:fontawesome-brands-github: Practicalli AstroNvim Config](http://github.com/practicalli/astronvim-config) is a clone of the AstroNvim user config with additional configuration to support Clojure development.

=== "Practicalli AstroNvim Config"
    Clone the [:fontawesome-brands-github: Practicalli AstroNvim config](https://github.com/practicalli/astronvim-config) which provides a user configuration with [Clojure support](clojure.md)
    !!! NOTE ""
        ```shell
        git clone http://github.com/practicalli/astronvim-config $HOME/.config/astronvim/lua/user
        ```
    Or clone to a separate directory and create a symbolic link
    !!! NOTE ""
        ```shell
        git clone http://github.com/practicalli/astronvim-config $HOME/.config/astronvim/lua/user \
        ln -s $HOME/.config/astronvim-config/ $HOME/.config/astronvim/lua/user
        ```

=== "AstroNvim User Config"
    Create your own user configuration using the AstroNvim user configuration template repository.

    Create a repository from the AstroNvim/user_example repository template

    ![AstroNvim user example repository - use this template](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-user-config-template-github-repository.png?raw=true){loading=lazy}

    Clone the newly created repository into the existing AstroNvim configuration, in a `user` directory
    ```shell
    git clone git@github.com/<github-account>/<new-repository> $HOME/.config/astronvim/lua/user
    ```

## Configure shell alias

[:fontawesome-solid-book-open: Configure shell alias](/neovim/configuration/){target=_blank .md-button}


## Post install

Open a terminal and use the `astro` alias to run Neovim.

!!! NOTE ""
    ```shell
    astro
    ```

<!-- TODO: checkhealth screenshot for astronvim -->

> `NVIM_APPNAME=astronvim nvim` to run Neovim with astronvim without setting a shell alias.

Neovim will open and display the Lazy plugin manager UI, showing the progress of plugin installation.  This should only happen on the first run.

### Check Health

Run the Neovim `:checkhealth` command to report on the general Neovim install and supporting tools

<!-- TODO: checkhealth screenshot for astronvim -->


### Add LSP DAP Lint and Format tools

`SPC p m` to launch Mason which manages LSP servers, linters, filters ...

![AstroNvim packages - mason all installed](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-packages-mason-installed-all.png?raw=true){loading=lazy}


### Configure format rules

The configuration files for each lint and format tool should be used by Neovim.

> Setting a different location for these files has proved challenging.  `plugin/null-ls.lua` has a section to override its builtin configuration for each lint and format tool, however, in tests Practicalli was unable to succeffuly set a different location.
