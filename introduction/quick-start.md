# Quick start

The briefest of summary on how to get started with Neovim and Clojure development.  See the [install section](/install/) for full details.

* [Install Neovim 7 or greater](https://github.com/neovim/neovim/wiki/Installing-Neovim)
* Install supporting tools
    * `tar` & `curl` and a C compiler, e.g. `gcc` for Linux or `clang` for android/termix (required by nvim-treesitter)
    * ripgrep to search for files (used by telescope)
* [Clone Neovim Config](https://github.com/practicalli/neovim-config-redux)
* Run `nvim` in a terminal and ignore the warning, press `RTN`
    * `:PackerInstall` command in Neovim
* [Install Clojure CLI](https://practical.li/clojure/clojure-cli/install/) (or Leiningen)
* Clone / fork [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn/) or add an alias with the [required config to use nrepl and cider-nrepl](https://github.com/Olical/conjure/wiki/Quick-start:-Clojure#with-clojure-cli)
* [Run a Clojure REPL process](/repl-driven-development/) - in a separate terminal session
   * `clojure -M:repl/rebel` for a rich REPL UI
   * `clojure -M:repl/cider` for a basic REPL UI
   * `clojure -M:repl/headless` for a headless REPL process
* Open a Clojure file in Neovim - Conjure will automatically connect


## Next Steps

[Learn how to use Neovim](/neovim-basics/) and how to [use Conjure for REPL driven development](/repl-driven-development/conjure.html)


## Ultra-mobile development

> [Termux section](/termux/) details how to set up full Clojure development environment on an Android smartphone
