# Install Clojure

A rich Clojure REPL workflow is provided by the Conjure package, which works with [Clojure CLI](#clojure-cli) and [Leiningen](#leiningen) projects, assuming the respective tool is installed.

Clojure LSP is highly recommended and packages to use an [installed clojure-lsp tool](#clojure-lsp) are the [practicalli/neovim-config](https://github.com/practicalli/neovim-config) configuration


## Clojure CLI

[Clojure CLI](https://clojure.org/guides/deps_and_cli) provides a way to run Clojure code, a packaged application (jar) and of course a REPL.

Adding community tools provides a configurable experience to support your Clojure development workflow.  [practicalli/clojure-deps-edn provides a wide range of tools](https://practical.li/clojure/clojure-cli/install/community-tools.html) that can easily be added to the development environment and used across all projects

Practicalli Clojure has [a detailed guide to installing Clojure and related tools for an enhanced developer workflow](https://practical.li/clojure/clojure-cli/install/).  Or visit the [Clojure Getting Started guide](https://clojure.org/guides/getting_started) for just the Clojure CLI.


## Clojure LSP

clj-kondo provides static analysis of source code files, providing subtle warnings as Clojure code is written to help the developer follow idioms and avoid syntatic errors.

Clojure LSP includes clj-kondo to provide [an implementation of the Language Server Protocol for the Clojure Language](https://clojure-lsp.io/).

Neovim can use and visualise information from the Clojure LSP server to assist with the development and refactor of Clojure code.

Follow the [Clojure LSP installation guide](https://clojure-lsp.io/)

Once installed, run `clojure-lsp -v` in a terminal to ensure the command is working.


## Leinigen

The large majority of existing Clojure projects have used Leiningen build automation tool (although there is a growing number of new projects using Clojure CLI as well or instead of Leiningen)

Follow the install instructions at [Leiningen.org](https://leiningen.org/)
