# Config Design - AstroNvim

[:globe_with_meridians: AstroNvim](https://astronvim.com/) is a community configuration with an engaging UI, using Lazy for plugin management (Neovim packages) and Mason for package management (LSP, DAP, format and lint tools)

[:fontawesome-brands-github: Practicalli AstroNvim User Config](https://github.com/practicalli/astro) is a user configuration that extends AstroNvim and imports packages from the [:fontawesome-brands-github: AstroNvim Community](https://github.com/AstroNvim/user_example).


## Neovim Configuration

Practicalli Neovim is based on [AstroNvim](astronvim/), a thoughtful configuration that supports the latest Neovim stable releases, provides a polished UI and many community extensions.

Practicalli AstroNvim User Config provides a complete Clojure config on top of AstroNvim.

[Install Practicalli AstroNvim Config](astronvim/index.md){.md-button} 


> NOTE: [Practicalli Neovim Config Redux](practicalli/) was a learning experiment that provided mnemonic key bindings, packer, telescope selector, written in Fennel.  This project has now been archived in favour of AstroNvim






### Configure format rules

The configuration files for each lint and format tool should be used by Neovim.

> Setting a different location for these files has proved challenging.  `plugin/null-ls.lua` has a section to override its builtin configuration for each lint and format tool, however, in tests Practicalli was unable to succeffuly set a different location.
