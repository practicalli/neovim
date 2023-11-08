# Install Overview

Practicalli Neovim provides a feature rich configuration for Neovim and all the tools required for effective Clojure development (and other Lisp dialects too).

- [Clojure tooling and a Java SDK](clojure.md) (Java Virtual Machine)
- [Neovim 0.9.x or nightly build](neovim.md)
- [Neovim package manager and packages](packages/index.md)
- [NerdFonts](https://www.nerdfonts.com/){target=_blank} for icon support in themes and status line
- Optional: [Neovide](neovide.md) GUI for neovim

!!! WARNING "Neovim 0.9.x latest stable release"
    Content and configuration in this book has been tested against Neovim 0.9.x over the summer of 2023

## Install summary

If you are familiar with most of the tools required, then the quick start list below provides an ultra-terse version on how to get started with Neovim and Clojure development.

- [Install Neovim 0.9.x or greater](https://github.com/neovim/neovim/wiki/Installing-Neovim){target=_blank}
    - [Linux AppImage](https://github.com/neovim/neovim/releases/){target=_blank}
    - `brew install --HEAD neovim` for Homebrew install of development version
- Install supporting tools
    - `tar` & `curl` and a C compiler, e.g. `gcc` for Linux or `clang` for android/termix (required by nvim-treesitter)
    - `ripgrep` & `fd` to search for files (used by telescope)
    - `luarocks` for LSP support in AstroNvim
- Optionally add a community configuration, e.g. [AstroNvim](/neovim/configuration/astronvim/){target=_blank} or [Practicalli Neovim Config](https://github.com/practicalli/neovim-config-redux){target=_blank}
- Run `nvim` in a terminal 
- [Install Clojure CLI](clojure.md) and supporting tools
- Clone / fork [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn/){target=_blank} or add an alias with the [required config to use nrepl and cider-nrepl](https://github.com/Olical/conjure/wiki/Quick-start:-Clojure#with-clojure-cli){target=_blank}
- [Run a Clojure REPL process](/repl-driven-development/) - in a terminal session with nREPL, e.g. using one of the REPL aliases from [practicalli/clojure-cli-config](https://github.com/practicalli/clojure-cli-config){target=_blank}
    - `clojure -M:repl/rebel` for a rich REPL UI with auto-completion & docs
    - `clojure -M:repl/headless` - headless REPL process when working exclusively in a Clojure connected editor
. Open a Clojure file in Neovim - Conjure will automatically connect


## Next Steps

[Learn how to use Neovim](../neovim-basics/) and how to [use Conjure for REPL driven development](../repl-driven-development/conjure.md)
