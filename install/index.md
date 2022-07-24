# Install Overview

Practicalli Neovim provides a feature rich configuration for Neovim and all the tools required for effective Clojure development (and other Lisp dialects too).

* [Clojure tooling and a Java SDK](clojure.md) (Java Virtual Machine)
* [Neovim 7 or nightly build](neovim.md)
* [Neovim package manager and packages](packages/index.md)
* [NerdFonts](https://www.nerdfonts.com/) for icon support in themes and status line


# Brief summary of install

If you are familiar with most of the tools required, then the quick start list below provides an ultra-terse version on how to get started with Neovim and Clojure development.

* [Install Neovim 7 or greater](https://github.com/neovim/neovim/wiki/Installing-Neovim) - development build recommended
    * [Ubuntu daily builds PPA](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable)
    * `brew install --HEAD neovim` for Homebrew install of development version
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




## Clojure

Conjure is the main Neovim plugin for Clojure, providing a REPL driven development workflow.

A Java OpenJDK install (e.g. [Eclipse Temurin](https://adoptium.net/), [AWS corretto](https://aws.amazon.com/corretto/)) is required to host Clojure applications.

Clojure CLI or Leiningen are tools that Conjure can use to start a Clojure REPL.

Clojure LSP server provides static analytics for Neovim LSP client to provide live linting of code as its written, aid with code refactor actions and supporting code writing tools.


## Neovim

Neovim 7 is the latest release and is recommended.

Or an Neovim pre-release or nightly build if you are feeling more adventurous.
