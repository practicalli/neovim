# Install Neovim

Neovim 7 is the minimum version for this configuration.  The latest release of Neovim 7 has been work well for Clojure development by the Practicalli team

Practicalli recommends using the latest release from [the Neovim releases page](https://github.com/neovim/neovim/releases)

Follow the [install Neovim guide for the specific operating system](https://github.com/neovim/neovim/wiki/Installing-Neovim).

> Update to a Neovim development build if there are issues with Treesitter and the nvim-treesitter package, as they are features under active development, e.g.  [Ubuntu daily builds PPA](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) or `brew install --HEAD neovim` for Homebrew


## Post Install checks

`nvim` in a terminal to run NeoVim and check the installation is working without error.

![NeoVim - default startup message](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-startup-default-message.png)

`:checkhealth` to run a check supporting libraries and tools are available to NeoVim.

A report is generated and shown in NeoVim

`j` / `k` to scroll through the checkhealth report

Review the warnings and follow any advice given to resolve the issues.

![NeoVim checkhealth report](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-checkhealth-report.png)


### Provider warnings & disable options

NeoVim and it packages may delegates features to language and tool specific [providers](https://neovim.io/doc/user/provider.html).

Resolve the issue with providers that generate a warning in the checkhealth report, following the ADVICE steps.

Or disable a specific provider if not required to remove the warning from the report. Details on how to disable a provider are included at the end of the ADVICE in the report section for that provider.

![NeoVim checkhealth report - python provider warning](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-checkhealth-warning-python.png)

So to disable the python provider, add `let g:loaded_python3_provider = 0` to the Neovim configuration.

> Each NeoVim package used should be checked to see if it requires a specific provider.
