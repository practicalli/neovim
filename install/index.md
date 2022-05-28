# Install Overview

A Clojure development environment within requires

* [Clojure tooling and a Java SDK](clojure.md) (Java Virtual Machine)
* [Neovim 7 or nightly build](neovim.md)
* [Neovim package manager and packages](packages/index.md)

Neovim and its packages may use external tools (providers) for some features.  So tools including node.js, python3, ruby, xclip, etc.


## Clojure

Conjure is the main Neovim plugin for Clojure, providing a REPL driven development workflow.

A Java OpenJDK install (e.g. [Eclipse Temurin](https://adoptium.net/), [AWS corretto](https://aws.amazon.com/corretto/)) is required to host Clojure applications.

Clojure CLI or Leiningen are tools that Conjure can use to start a Clojure REPL.

Clojure LSP server provides static analytics for Neovim LSP client to provide live linting of code as its written, aid with code refactor actions and supporting code writing tools.


## Neovim

Neovim 7 is the latest release and is recommended.

Or an Neovim pre-release or nightly build if you are feeling more adventurous.



### Package Manager

[Packer](https://github.com/wbthomason/packer.nvim) is a [`use-package`](https://github.com/jwiegley/use-package) inspired package management for Neovim.

Packer is used as the package manager in this guide as it is built on native packages, see `:h packages`, is written and configured in Lua (although Fennel will be used where possible) and supports Luarocks dependencies.

Other features of packer include:

- Declarative plugin specification
- Support for dependencies
- Expressive configuration and lazy-loading options to improve startup time
- Post-install/update hooks
- Uses jobs for async installation
- Support for `git` tags, branches, revisions, submodules
- Support for local plugins

<!-- TODO: > See the package manager comparison in reference section  -->


### Packages

Neovim packages add extra functionality to Neovim, e.g. conjure package provides an excellent Clojure REPL experience (and supports several other languages too).

See the packages section for details of the packages used and a breakdown of their configuration.

 list chosen
- alternatives that could be used (add to reference section)
