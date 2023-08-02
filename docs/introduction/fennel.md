# Fennel configuration

Practicalli uses Fennel to define all configuration for Neovim.  Fennel is a LISP dialect and should quickly become comfortable to Clojure developers.

Lua is the defacto language to configuring Neovim and for plugin development and neovim packages written in lua are preferred over those in Vimscript, assuming a Fennel package is not available.

Although Neovim fully supports Vimscript, Practicalli encourages Fennel or Lua, as Vimscript is quite a niche language and quite complex syntax.


## Fennel Overview

![Fennel Language logo](https://fennel-lang.org/logo.svg){align=right loading=lazy}

[Fennel](https://fennel-lang.org/){target=_blank} is a programming language that brings together the speed, simplicity, and reach of [Lua](https://www.lua.org/){target=_blank} with the flexibility of a [lisp syntax and macro system.](https://en.wikipedia.org/wiki/Lisp_(programming_language)){target=_blank}

* Full Lua compatibility: Easily call any Lua function or library from Fennel and vice-versa.
* Zero overhead: Compiled code should be just as efficient as hand-written Lua.
* Compile-time macros: Ship compiled code with no runtime dependency on Fennel.
* Embeddable: Fennel is a one-file library as well as an executable. Embed it in other programs to support runtime extensibility and interactive development.

Anywhere you can run Lua code, you can run Fennel code.

!!! TIP "Translate Lua to Fennel"
    [See Fennel](https://fennel-lang.org/see){target=_blank} is an online antifennel tool to convert Lua to Fennel or Fennel to Lua.

    [practicalli/neovim-config-redux configuration](https://github.com/practicalli/neovim-config-redux){target=_blank} provides helper functions to minimise the translation required.


## Fennel Packages

The Conjure package which provides the Clojure REPL (and much more) is written in Fennel.


## Runtime conversion

Fennel is converted to Lua using the aniseed package

Aniseed bridges the gap between [Fennel](https://fennel-lang.org/){target=_blank} (a Lisp that compiles to Lua) and [Neovim](https://neovim.io/){target=_blank}. Allowing you to easily write plugins or configuration in a [Clojure](https://clojure.org/){target=_blank} like Lisp with great runtime performance.


## Development tooling

Neovim support

* [Anti-fennel](https://git.sr.ht/~technomancy/antifennel){target=_blank} - convert from Lua code to Fennel code.
* [aniseed](https://github.com/Olical/aniseed){target=_blank} - write plugins or configuration for Neovim with great runtime performance
* [hotpot](https://github.com/rktjmp/hotpot.nvim){target=_blank} - seamless Fennel inside Neovim

[See Fennel](https://fennel-lang.org/see){target=_blank} is an online antifennel tool to convert between Lua and Fennel.

[Guide to plugin development with fennel](https://russtoku.github.io/posts/nfnl-experience.html){target=_blank .md-button}


Emacs support:

* [technomancy/fennel-mode](https://git.sr.ht/~technomancy/fennel-mode){target=_blank} and [Emacs mirror repository](https://github.com/emacsmirror/fennel-mode){target=_blank}


## Playing Games

[TIC-80](https://tic80.com/){target=_blank} is a simulated computer environment to to write code, design art, compose music and retro style game games.

[LÖVE](https://love2d.org/){target=_blank} is a framework for making games with the Lua programming language, allows import from external resources and can use any resolution or memory resources required.

TIC-80 and LÖVE provide cross-platform support across Windows, Mac and Linux systems. TIC-80 games can also be played in the browser.
