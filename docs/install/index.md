# Install Overview

Practicalli Neovim provides a feature rich configuration for Neovim and all the tools required for effective Clojure development (and other Lisp dialects too).

* [Clojure tooling and a Java SDK](clojure.md) (Java Virtual Machine)
* [Neovim 8 or nightly build](neovim.md)
* [Neovim package manager and packages](packages/index.md)
* [NerdFonts](https://www.nerdfonts.com/){target=_blank} for icon support in themes and status line


## Install summary

If you are familiar with most of the tools required, then the quick start list below provides an ultra-terse version on how to get started with Neovim and Clojure development.

* [Install Neovim 8 or greater](https://github.com/neovim/neovim/wiki/Installing-Neovim){target=_blank} - development build recommended
    * [Ubuntu daily builds PPA](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable){target=_blank}
    * `brew install --HEAD neovim` for Homebrew install of development version
* Install supporting tools
    * `tar` & `curl` and a C compiler, e.g. `gcc` for Linux or `clang` for android/termix (required by nvim-treesitter)
    * ripgrep to search for files (used by telescope)
* [Clone Neovim Config](https://github.com/practicalli/neovim-config-redux){target=_blank}
* Run `nvim` in a terminal and ignore warnings, press `RTN`
    * `SPC P i` or `:PackerInstall` command in Neovim to install packages
* [Install Clojure CLI](clojure.md) and supporting tools
* Clone / fork [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn/){target=_blank} or add an alias with the [required config to use nrepl and cider-nrepl](https://github.com/Olical/conjure/wiki/Quick-start:-Clojure#with-clojure-cli){target=_blank}
* [Run a Clojure REPL process](/repl-driven-development/) - in a terminal session with nREPL, e.g. using one of the REPL aliases from [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn){target=_blank}
    * `clojure -M:repl/rebel` for a rich REPL UI with auto-completion & docs
    * `clojure -M:repl/headless` - headless REPL process when working exclusively in a Clojure connected editor
* Open a Clojure file in Neovim - Conjure will automatically connect


## Next Steps

[Learn how to use Neovim](/neovim-basics/) and how to [use Conjure for REPL driven development](/repl-driven-development/conjure.html)
