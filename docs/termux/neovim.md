# Install neovim

Neovim version 9.5 is currenlyt available as a Termux package

```
pkg install neovim
```

<!-- TODO: Is there a PPA for development version of Neovim? -->


## Neovim treesitter

Treesitter provides excellent language syntax parsing and highlighting performance, allowing any Neovim package to benefit.

The `nvim-treesitter` package is included in the [practicalli/astro](https://github.com/practicalli/astro){target=_blank} configuration.


## C Compiler

Install C compiler to compile the parser for each specific programming language.

```
pkg install clang
```

> `gcc` is not packaged for Termux, although there are guides to install gcc if preferred. clang has proved to be capable of creating the parsers used in the Practicalli configuration.


### Searching files

Telescope and other packages that involve searching for files recommend using ripgrep, a highly optomised tool for finding files on the operating system.

```
pkg install ripgrep
```


## [optional] nodejs

Optional.  Only if node.js is required as a Neovim provider and JavaScript or ClojureScript development is to be done.

```
pkg install nodejs
```
