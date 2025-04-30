# Practicalli Astro 5 Config

![Practicalli Logo](https://github.com/practicalli/graphic-design/blob/live/logos/practicalli-logo.png?raw=true#only-light){align=right loading=lazy style="height:72px"}
![Practicalli Logo](https://github.com/practicalli/graphic-design/blob/live/logos/practicalli-logo-dark.png?raw=true#only-dark){align=right loading=lazy style="height:72px"}

[:fontawesome-brands-github: Practicalli Astro 5](http://github.com/practicalli/nvim-astro5) is Clojure development focused configuration, an extension of the [:fontawesome-brands-github: AstroNvim v5 template repository](https://github.com/AstroNvim/template).

=== "Only One Neovim Config"

    Clone the [:fontawesome-brands-github: Practicalli Astro](https://github.com/practicalli/nvim-astro5) configuration or create your own fork and clone that repository.


    !!! NOTE "Clone Practicalli Astro config"
        ```shell
        git clone https://github.com/practicalli/nvim-astro5.git ~/.config/nvim
        ```

=== "Multiple Neovim Configurations"
    Clone the [:fontawesome-brands-github: Practicalli Astro](https://github.com/practicalli/nvim-astro5) configuration to a unique name within `~/.config` directory.

    ```shell
    git clone https://github.com/practicalli/astro5.git ~/.config/nvim-astro5
    ```

    Set the `NVIM_APPNAME` environment variable to the configuration directory name under `~/.config`

    e.g. Run Neovim using the configuration in `~/.config/astro5`
    ```shell
    export NVIM_APPNAME=nvim-astro5 nvim
    ```

    [:fontawesome-solid-book-open: Configure shell alias and selectors](multiple-configurations.md){target=_blank} to simplify the command to run a specific configuration.


??? INFO "Practicalli Astro 5 Design guide"
    [Practicalli Astro 5 design & override guide](/neovim/reference/configuration/){target=_blank .md-button}


## Install Neovim Plugins

Enter `nvim` command in a terminal to launch Neovim and install all the plugins from the Practicalli Astro 5 configuration.

!!! NOTE "Run Neovim"
    ```shell
    nvim
    ```

Lazy plugin manager runs automatically and installs all the plugins defined in the Neovim configuration.

Treesitter will prompt to compile its language parsers.

++"q"++ to close the lazy package manager pop-up once all plugins are installed.


??? INFO "Plugin install without UI display"
    Use the `--headless` Neovim flag to install plugins without running whole Neovim editor user interface.

    ```shell
    nvim --headless
    ```

??? TIP "Identical install with lazy-lock.json"
    `lazy-lock.json` contains the versions of all plugins currently installed. Use this file if you need exact plugin versions as part of other installs.  Otherwise ignore it.

## Post Install checks

Troubleshoot the Neovim configuration and supporting tools by running the [:globe_with_meridians: Neovim Heath Check](https://neovim.io/doc/user/health.html){target=_blank}.

Use the `:checkhealth` command in Neovim or start Neovim with the Health Check command.

!!! EXAMPLE "Run Neovim and start Health Check"
    ```shell
    nvim +:checkhealth
    ```

A report is generated and shown in Neovim

++"j"++ / ++"j"++ to scroll through the checkhealth report

Review the warnings and install tooling that is required for languages that will be used.

![NeoVim checkhealth report](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-checkhealth-report-light.png?raw=true#only-light)
![NeoVim checkhealth report](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-checkhealth-report-dark.png?raw=true#only-dark)

!!! HINT "Ignore Provider Warnings"
    It is safe to ignore language provider warnings.

    [Language Providers can be disabled](/neovim/reference/neovim/language-providers/) in the Neovim configuration to remove the warnings from `:checkhealth` report.
