# Practicalli Nvim-Astro Config

![Practicalli Logo](https://github.com/practicalli/graphic-design/blob/live/logos/practicalli-logo.png?raw=true#only-light){align=right loading=lazy style="height:72px"}
![Practicalli Logo](https://github.com/practicalli/graphic-design/blob/live/logos/practicalli-logo-dark.png?raw=true#only-dark){align=right loading=lazy style="height:72px"}

[:fontawesome-brands-github: Practicalli Nvim-Astro](http://github.com/practicalli/nvim-astro) is Clojure development focused configuration, an extension of the [:fontawesome-brands-github: AstroNvim v6 template repository](https://github.com/AstroNvim/template).

=== "Only One Neovim Config"

    Clone the [:fontawesome-brands-github: Practicalli Astro](https://github.com/practicalli/nvim-astro) configuration or create your own fork and clone that repository.


    !!! NOTE "Clone Practicalli Nvim-Astro config"
        ```shell
        git clone https://github.com/practicalli/nvim-astro.git ~/.config/nvim
        ```

=== "Multiple Neovim Configurations"

    Clone the [:fontawesome-brands-github: Practicalli Nvim-Astro](https://github.com/practicalli/nvim-astro) configuration to a unique name within `~/.config` directory.

    !!! NOTE "Clone Practicalli Nvim-Astro config to unique config name"
        ```shell
        git clone https://github.com/practicalli/astro.git ~/.config/nvim-astro
        ```

    Set the `NVIM_APPNAME` environment variable to the configuration directory name under `~/.config`, e.g. Run Neovim using the configuration in `~/.config/nvim-astro`

    !!! NOTE "Create Shell Alias to use Nvim-Astro config with Neovim"
        ```shell
        export NVIM_APPNAME=nvim-astro nvim
        ```

    [:fontawesome-solid-book-open: Configure shell alias and selectors](multiple-configurations.md){target=_blank} to simplify the command to run a specific configuration.


[Customise Practicalli Nvim-Astro](customise-configuration.md){target=_blank .md-button}


## Install Neovim Plugins

Run Neovim in a terminal and all the plugins and supporting Mason tools from the Practicalli Nvim-Astro configuration will be installed. Treesitter parsers for all supported languages are installed too.

!!! NOTE "Run Neovim"
    With a single Neovim Config, use the `nvim` command in a terminal

    ```shell
    nvim
    ```

    With multiple configurations, use a shell alias or set the `NVIM_APPNAME` to set the preferred configuration.  For example, with Nvim-Astro, use the `astro` alias.

    ```shell
    astro
    ```

Lazy plugin manager runs automatically and installs all the plugins defined in the Neovim configuration.

Mason runs and installs tools that are defined in the configuration.

Treesitter will compile all the language parsers.

++"q"++ to close the lazy package manager pop-up once all plugins are installed.

!!! TIP "Breaking Changes - update packages again"
    If a "Breaking Changes" section is shown when adding or updating plugins in the Lazy popup, press ++"U"++ key to update again until no more breaking changes show.


??? WARNING "Avoid running Nvim-Astro package update headless"
    Do not use the `--headless` Neovim flag to install plugins or pass the `+:Lazy update` arguments.  The Lazy.nvim package manager requires neovim UI to run correctly.


??? TIP "Identical install with lazy-lock.json"
    When plugins are installed, a `lazy-lock.json` contains the versions of all plugins. Include this file when exact plugin versions are required for other system installs.  Otherwise this file can be safely ignored.


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

[Troubleshoot Neovim Configuration](troubleshoot.md){target=_blank .md-button}
