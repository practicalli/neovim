# Install Clojure

A rich Clojure REPL workflow is provided by the Conjure package, which works with [Clojure CLI](#clojure-cli) and [Leiningen](#leiningen) projects, assuming the respective tool is installed.

Clojure LSP is highly recommended and packages to use an [installed clojure-lsp tool](#clojure-lsp) are in the [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) configuration


## Clojure CLI

[:globe_with_meridians: Practicalli Clojure install guide](https://practical.li/clojure/install/){target=_blank .md-button}

[:globe_with_meridians: Clojure CLI](https://clojure.org/guides/deps_and_cli){target=_blank} provides a way to run Clojure code, packaged Clojure (jar) and run a Clojure REPL.

[:globe_with_meridians: Practicalli Clojure install guide](https://practical.li/clojure/install/){target=_blank} details prerequisites, Clojure install options and supporting tools for an enhanced developer workflow.

> Visit the [:globe_with_meridians: Clojure Getting Started guide](https://clojure.org/guides/getting_started){target=_blank} for the Clojure CLI or to check the latest release version.

[:globe_with_meridians: Practicalli Clojure CLI Config](https://practical.li/clojure/clojure-cli/practicalli-config/){target=_blank} provides a wide range of community tools that extend the features of Clojure CLI, creating a rich development environment for use across all projects.

!!! WARNING "Aliases are required for many examples"
    Without [:globe_with_meridians: Practicalli Clojure CLI Config](https://practical.li/clojure/install/clojure-cli/#practicalli-clojure-cli-config){target=_blank} many commands provided in this book are not available unless similar alias definitions are added to a either a project or user level `deps.edn` configuration.


## Language Server Protocol

Neovim Treesitter surfaces information from Language Server Protocol (LSP) servers to assist with development and refactor of Clojure code.

[:globe_with_meridians: Clojure LSP installation guide](https://clojure-lsp.io/installation/) shows how to install the Clojure LSP binary for the relevant operating system.

Once installed, run `clojure-lsp -v` in a terminal to ensure the command is working.

!!! HINT "practicalli/clojure-lsp-config"
    [:fontawesome-brands-github: practicalli/clojure-lsp-config](https://github.com/practicalli/clojure-lsp-config) provides a complete configuration for clojure-lsp (`config.edn`), including a wide range of snippets and less restrictive formatting rules (`cljfmt.edn`)

> clj-kondo provides static analysis of source code files, providing subtle warnings as Clojure code is written to help the developer follow idioms and avoid syntatic errors.
>
> Clojure LSP includes clj-kondo to provide [:globe_with_meridians: an implementation of the Language Server Protocol for the Clojure Language](https://clojure-lsp.io/){target=_blank}.

[:globe_with_meridians: Clojure LSP installation guide](https://clojure-lsp.io/installation/){target=_blank .md-button }
[:fontawesome-solid-book-open: Treesitter Fennel Configuration](/neovim/install/configuration/#fnlconfigplugintreesitterfnl){target=_blank .md-button}


## Leiningen

Many existing Clojure projects use Leiningen build automation tool (although many new projects use Clojure CLI as well or instead of Leiningen).  

The code is the same regardless of tooling choice.  The overall workflow is the same, although Clojure CLI may provide more workflow options.

Follow the install instructions at [Leiningen.org](https://leiningen.org/){target=_blank} if required.
