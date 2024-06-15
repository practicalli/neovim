# Fennel

![Fennel Language logo](https://fennel-lang.org/logo.svg){align=right loading=lazy style="height:150px;width:150px"}

Lua is the defacto language for Neovim plugin development and configuration.

Fennel can be used to write Neovim packages and configuration, using [:fontawesome-brands-github: nfnl](https://github.com/Olical/nfnl) to generate the equivalent Lua code that Neovim runs.

> Although Neovim fully supports Vimscript, Practicalli encourages Fennel or Lua, as Vimscript is a niche language with quite complex syntax.


## Overview

[:fontawesome-solid-globe: Fennel](https://fennel-lang.org/){target=_blank} is a programming language that brings together the speed, simplicity, and reach of [:fontawesome-solid-globe: Lua](https://www.lua.org/){target=_blank} with the flexibility of a [:fontawesome-solid-globe: lisp syntax and macro system.](https://en.wikipedia.org/wiki/Lisp_(programming_language)){target=_blank}

* Full Lua compatibility: Easily call any Lua function or library from Fennel and vice-versa.
* Zero overhead: Compiled code should be just as efficient as hand-written Lua.
* Compile-time macros: Ship compiled code with no runtime dependency on Fennel.
* Embeddable: Fennel is a one-file library as well as an executable. Embed it in other programs to support runtime extensibility and interactive development.

Anywhere you can run Lua code, you can run Fennel code.

!!! TIP "Translate Lua to Fennel"
    [:fontawesome-solid-globe: See Fennel](https://fennel-lang.org/see){target=_blank} is an online antifennel tool to convert Lua to Fennel or Fennel to Lua.

    [practicalli/neovim-config-redux configuration](https://github.com/practicalli/neovim-config-redux){target=_blank} provides helper functions to minimise the translation required.


## Fennel Packages

The Conjure package which provides the Clojure REPL (and much more) is written in Fennel.


## nfnl

[:fontawesome-brands-github: nfnl](https://github.com/Olical/nfnl) generates Lua code from Fennel code.  Neovim runs the generated Lua code.

nfnl loads only when working in directories containing a `.nfnl.fnl` configuration file, so has zero overhead when not working with fennel.

`*.fnl` files are automatically compiled to `*.lua` when changes are saved, showing any compilation errors to provide an effective feedback loop.

[nfnl standard library](https://github.com/Olical/nfnl/tree/main/docs/api/nfnl){target=_blank .md-button}

[nfnl plugin example](https://github.com/Olical/nfnl-plugin-example){target=_blank .md-button}


## Development tooling

Neovim support

* [Anti-fennel](https://git.sr.ht/~technomancy/antifennel){target=_blank} - convert from Lua code to Fennel code.
* [nfnl](https://github.com/Olical/nfnl){target=_blank} - write plugins or configuration for Neovim with great runtime performance
* [hotpot](https://github.com/rktjmp/hotpot.nvim){target=_blank} - seamless Fennel inside Neovim

[:fontawesome-solid-globe: See Fennel](https://fennel-lang.org/see){target=_blank} is an online antifennel tool to convert between Lua and Fennel.

[:fontawesome-solid-globe: Guide to plugin development with fennel](https://russtoku.github.io/posts/nfnl-experience.html){target=_blank .md-button}


Emacs support:

* [:fontawesome-solid-globe: technomancy/fennel-mode](https://git.sr.ht/~technomancy/fennel-mode){target=_blank} and [Emacs mirror repository](https://github.com/emacsmirror/fennel-mode){target=_blank}


## Playing Games

[:fontawesome-solid-globe: TIC-80](https://tic80.com/){target=_blank} is a simulated computer environment to to write code, design art, compose music and retro style game games.

[:fontawesome-solid-globe: LÖVE](https://love2d.org/){target=_blank} is a framework for making games with the Lua programming language, allows import from external resources and can use any resolution or memory resources required.

TIC-80 and LÖVE provide cross-platform support across Windows, Mac and Linux systems. TIC-80 games can also be played in the browser.
