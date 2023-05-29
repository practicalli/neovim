# Community Configuration Projects

Practicalli Neovim book covers the following configurations:


## Practicalli Neovim Config Redux

[:fontawesome-solid-book-open: Practicalli Neovim Config Redux](/neovim/configuration/practicalli/)

* Fennel configuration
* Packer package manager & Treesitter support
* Mnemonic key bindings
* Telescope selectors
* Autocompletion (cmp) & snippets (luasnip)
* Esc with center row keys, e.g. "fd"

## AstroNvim and Practicalli AstroNvim Config

[:fontawesome-solid-book-open: AstroNvim and Practicalli AstroNvim Config](/neovim/configuration/astronvim.md) organised configuration with a polished UI

* Neovim 9 support
* Lazy for plugins (packages for Neovim)
* Mason to manage install for LSP, DAP, lint and format tools
* Treesitter and language parser support
* Telescope selectors
* Notification dialogs
* Autocompletion (cmp) & snippets (luasnip)
* Neovim 9 background switch (live toggle light & dark theme)
* Hidden command line `cmdheight=0` (Neovim 0.8 onward)
* Esc with center row keys, e.g. "fd" (user: `plugins/core.lua`)

## Alternative configurations

Practicalli Neovim does not cover the following Community configurations.

* [Magit Kit](https://github.com/Olical/magic-kit) fennel configuration from the author of Conjure
* [cajus-nvim](https://github.com/rafaeldelboni/cajus-nvim) inspiration for practicalli/neovim-config-redux
* [LazyVim](https://www.lazyvim.org/) lazy & mason configuration
* [NvChad](https://github.com/NvChad/NvChad) polished UI with Lazy optomisations

!!! INFO "Long term project: Fennel config with AstroNvim-like UI experience"
    A very long term goal for Practicalli is to create a Neovim configuration written predominatly in Fennel, providing a rich user experience on par with the very polished experience of AstroNvim.

    Lazy and Mason should be used to manage packages and tools (LSP & DAP servers, lint & format tools).

    Which-key should provide a mnemonic menu system similar to the Spacemacs experience.
