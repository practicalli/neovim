# AstroNvim

[:globe_with_meridians: AstroNvim](https://astronvim.com/) is a community configuration with an engaging UI, using Lazy for plugin management (Neovim packages) and Mason for package management (LSP, DAP, format and lint tools)

[:fontawesome-brands-github: Practicalli AstroNvim User Config](https://github.com/practicalli/astronvim-user-config) is a user configuration that extends AstroNvim and imports packages from the [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/user_example).


## AstroNvim Install

[:fontawesome-brands-github: Practicalli AstroNvim User Config](http://github.com/practicalli/astronvim-user-config) is Clojure development focused configuration, an extension of the AstroNvim template.

[:fontawesome-brands-github: AstroNvim template repository](https://github.com/AstroNvim/template) provide a general configuration for Neovim. [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/astrocommunity/) provides plugin configs to make it easier to extend the general feature of AstroNvim.


=== "Practicalli AstroNvim User Config"
    Clone the [:fontawesome-brands-github: Practicalli AstroNvim User Config](https://github.com/practicalli/astronvim-user-config) which provides [Clojure support](clojure.md) on top of AstroNvim.
    !!! NOTE ""
        ```shell
        git clone http://github.com/practicalli/astronvim-user-config $HOME/.config/astronvim
        ```

=== "AstroNvim template"
    Create your own user configuration using the [:fontawesome-brands-github: AstroNvim template repository](https://github.com/AstroNvim/template) to create a new GitHub repository.

    Clone the newly created repository

    !!! NOTE ""
    ```shell
    git clone git@github.com/AstroNvim/template $HOME/.config/astronvim
    ```


!!! HINT "Use Shell Aliases if using multiple Neovim configurations"
    [:fontawesome-solid-book-open: Configure shell alias](/neovim/configuration/#configure-shell-alias){target=_blank .md-button}


## Post install

Open a terminal and use the `astro` alias to run Neovim.

!!! NOTE ""
    ```shell
    astro
    ```

Lazy package manager will run automatically and download all plugins.  Treesitter languages are automatically installed.  

++"q"++ to close the lazy package manager popup.

<!-- TODO: checkhealth screenshot for astronvim -->

> `NVIM_APPNAME=astronvim4 nvim` to run Neovim with astronvim without setting a shell alias.

Neovim will open and display the Lazy plugin manager UI, showing the progress of plugin installation.  This should only happen on the first run.

??? INFO "Unattended post install"
    Plugins can be installed without running the Neovim editor UI
    !!! NOTE ""
        ```shell
        NVIM_APPNAME=astronvim4 nvim --headless
        ```


### Check Health

Run the Neovim `:checkhealth` command to report on the general Neovim install and supporting tools

<!-- TODO: checkhealth screenshot for astronvim -->


### Add LSP DAP Lint and Format tools

`SPC p m` to launch Mason which manages LSP servers, linters, filters ...

![AstroNvim packages - mason all installed](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-packages-mason-installed-all.png?raw=true){loading=lazy}


### Configure format rules

The configuration files for each lint and format tool should be used by Neovim.

> Setting a different location for these files has proved challenging.  `plugin/null-ls.lua` has a section to override its builtin configuration for each lint and format tool, however, in tests Practicalli was unable to succeffuly set a different location.
