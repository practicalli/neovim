# Install neovim

Neovim version 0.11 is currently available as a Termux package

```
pkg install neovim
```

## Neovim config

[Practicalli Astro 5 config](/neovim/install/astro5-configuration/) provides tools for an effective Clojure workflow and software engineering tasks.


## Treesitter language support

Treesitter provides excellent language syntax parsing and highlighting performance, allowing any Neovim package to benefit.

Install C compiler to compile the parser for each specific programming language.

```shell
pkg install clang
```

> NOTE: `gcc` is not packaged for Termux, although there are guides to install gcc if preferred. clang has proved to be capable of creating the parsers used in the Practicalli configuration.


## Searching files

ripgrep is a highly optomised tool to search through files on the operating system, used by system pickers to optomise search results.

```shell
pkg install ripgrep
```


## LSP language servers

Some LSP servers require node.js to install and run.

```shell
pkg install nodejs
```
