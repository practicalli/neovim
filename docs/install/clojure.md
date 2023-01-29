# Install Clojure

A rich Clojure REPL workflow is provided by the Conjure package, which works with [Clojure CLI](#clojure-cli) and [Leiningen](#leiningen) projects, assuming the respective tool is installed.

Clojure LSP is highly recommended and packages to use an [installed clojure-lsp tool](#clojure-lsp) are in the [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) configuration


## Clojure CLI

[Practicalli Clojure install guide](https://practical.li/clojure/install/){target=_blank .md-button}

[Clojure CLI](https://clojure.org/guides/deps_and_cli){target=_blank} provides a way to run Clojure code, packaged Clojure (jar) and of course run a Clojure REPL.

[Practicalli Clojure install guide](https://practical.li/clojure/install/){target=_blank} details prerequisites, Clojure install options and supporting tools for an enhanced developer workflow.

> Visit the [Clojure Getting Started guide](https://clojure.org/guides/getting_started){target=_blank} for the Clojure CLI or to check the latest release version.

[Practicalli Clojure CLI Config](https://practical.li/clojure/clojure-cli/install/community-tools.html){target=_blank} provides a wide range of community tools that extend the features of Clojure CLI, creating a rich development environment for use across all projects.

!!! WARNING "Aliases are required for many examples"
    Without [Practicalli Clojure CLI Config](https://practical.li/clojure/install/clojure-cli/#practicalli-clojure-cli-config){target=_blank} many commands provided in this book are not available unless similar alias definitions are added to a either a project or user level `deps.edn` configuration.


## Clojure LSP

[Clojure LSP installation guide](https://clojure-lsp.io/){target=_blank .md-button }
[Treesitter Fennel Configuration](/neovim/install/configuration/#fnlconfigplugintreesitterfnl){target=_blank .md-button}

clj-kondo provides static analysis of source code files, providing subtle warnings as Clojure code is written to help the developer follow idioms and avoid syntatic errors.

Clojure LSP includes clj-kondo to provide [an implementation of the Language Server Protocol for the Clojure Language](https://clojure-lsp.io/){target=_blank}.

Neovim Treesitter uses and visualises information from the Clojure LSP server to assist with development and refactor of Clojure code.

Once installed, run `clojure-lsp -v` in a terminal to ensure the command is working.

!!! HINT "practicalli/clojure-lsp-config"
    [practicalli/clojure-lsp-config](https://github.com/practicalli/clojure-lsp-config) provides a complete configuration for clojure-lsp (`config.edn`), including a wide range of snippets and less restrictive formatting rules (`cljfmt.edn`)


## Leinigen

Many existing Clojure projects have used Leiningen build automation tool (although there is a growing number of new projects using Clojure CLI as well or instead of Leiningen)

Follow the install instructions at [Leiningen.org](https://leiningen.org/){target=_blank} if required.
