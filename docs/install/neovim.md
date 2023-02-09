# Install Neovim

[Neovim releases](https://github.com/neovim/neovim/releases){target=_blank .md-button}

Neovim 8 is the minimum version for this configuration.  The latest release of Neovim 7 has been work well for Clojure development by the Practicalli team

Practicalli recommends using the latest release from [the Neovim releases page](https://github.com/neovim/neovim/releases){target=_blank}

Follow the [install Neovim guide for the specific operating system](https://github.com/neovim/neovim/wiki/Installing-Neovim){target=_blank}.

> Update to a Neovim development build if there are issues with Treesitter and the nvim-treesitter package, as they are features under active development, e.g.  [Ubuntu daily builds PPA](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable){target=_blank} or `brew install --HEAD neovim` for Homebrew


## Post Install checks

Ensure supporting tools and binaries are available in the operating system by running the Neovim Heath Check.

`nvim` in a terminal to run NeoVim and check the installation is working without error.

![NeoVim - default startup message](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-startup-default-message.png){target=_blank}

`:checkhealth` to run a check supporting tools are available to NeoVim.

A report is generated and shown in NeoVim

`j` / `k` to scroll through the checkhealth report

Review the warnings and install tooling that is required for languages that will be used.

![NeoVim checkhealth report](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-checkhealth-report.png)

!!! HINT "Ignore Provider Warnings"
    It is safe to ignore language provider warnings.

    [Language Providers can be disabled](/neovim/reference/neovim/language-providers/) in the Neovim configuration to remove the warnings from `:checkhealth` report.  Examples of disabling language provders are in the [practicalli/neovim-config-redux configuration](https://github.com/practicalli/neovim-config-redux){target=_blank}, covered in the [Neovim Config](configuration/) install step
