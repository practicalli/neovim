# Fennel configuration

Practicalli uses Fennel to define all configuration for Neovim.  Fennel is a LISP dialect and should quickly become comfortable to Clojure developers.

Lua is the defacto language for configuring Neovim and plugin development, although converting between Lua examples to Fennel is relatively simple.

Neovim fully supports Vimscript, although it is felt that this is a relatively hard to understand way of configuring neovim and will not be used if at all possible.

![Fennel Language logo](https://fennel-lang.org/logo.svg)


# Fennel

Important packages used in this guide are written in Fennel, especially the excellent Conjure package that provides the Clojure REPL (and support for several other language environments).

[Fennel](https://fennel-lang.org/) is a programming language that brings together the speed, simplicity, and reach of [Lua](https://www.lua.org/) with the flexibility of a [lisp syntax and macro system.](https://en.wikipedia.org/wiki/Lisp_(programming_language))

* Full Lua compatibility: Easily call any Lua function or library from Fennel and vice-versa.
* Zero overhead: Compiled code should be just as efficient as hand-written Lua.
* Compile-time macros: Ship compiled code with no runtime dependency on Fennel.
* Embeddable: Fennel is a one-file library as well as an executable. Embed it in other programs to support runtime extensibility and interactive development.

Anywhere you can run Lua code, you can run Fennel code.


## Fennel to Lua

Lua is the defacto language for writing Neovim packages, although there are more developers seeing Fennel as a viable alternative.

Fennel is converted to Lua using the aniseed package

Aniseed bridges the gap between [Fennel](https://fennel-lang.org/) (a Lisp that compiles to Lua) and [Neovim](https://neovim.io/). Allowing you to easily write plugins or configuration in a [Clojure](https://clojure.org/)-like Lisp with great runtime performance.


## Lua to Fennel

Neovim package configuration is typically provided in Lua code, so requires translation into fennel.  Although this conversion should be fairly straightforward, [Anti-fennel](https://git.sr.ht/~technomancy/antifennel) can converts Lua code into Fennel code.

[See Fennel](https://fennel-lang.org/see) is an online antifennel tool to convert between Lua and Fennel.


## Development tooling

Neovim support

* [aniseed](https://github.com/Olical/aniseed) - write plugins or configuration for Neovim with great runtime performance
* [hotpot](https://github.com/rktjmp/hotpot.nvim) - seamless Fennel inside Neovim

Emacs support:

* https://git.sr.ht/~technomancy/fennel-mode
* https://github.com/emacsmirror/fennel-mode


## Playing Games

[TIC-80](https://tic80.com/) is a simulated computer environment to to write code, design art, compose music and retro style game games.

[LÖVE](https://love2d.org/) is a game-making framework for the Lua programming language and can beas Fennel compiles to Lua, you can reference the LÖVE wiki when making games with Fennel. LÖVE is more flexible than TIC-80 in that it allows you to import from external resources and use any resolution or memory you like, but at a cost in that it is more complicated to make games in.

TIC-80 and LÖVE provide cross-platform support across Windows, Mac and Linux systems. TIC-80 games can also be played in the browser.
