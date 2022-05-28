# Introduction

Neovim is a highly extensible and powerful editor, supporting mult-modal editing and Vim-style key bindings.

Practicalli Neovim will guide you through installing Clojure and Neovim and how to use them for a simple, powerful and fun REPL Driven Development workflow

![Clojure REPL Driven Development workflow](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/clojure-repl-driven-development-lifecycle-concept.png)


## Quickstart



## Distraction Free workflow experience

A clean UI provides for a distraction free development experience, with only the essential information presented in the Neovim statusline or inline with the code

* statusline - REPL / LSP status, editing mode, cursor position (line/column)
* line numbers - relative linenumbers (visual - skip wrapped lines)
* Inline with code (live lint feedback, LSP code lense references and unit test coverage)
* at the cursor (autocomplete, snippets)

> Clojure LSP code analysis kept to a minimum, discussing optional feedback that can be enabled (doc popups, etc.)


## Practicalli Approach

Practicalli recommends using Fennel as the first option for writing Neovim configuration, as Fennel is a LISP dialect and should therefore be relatively familiar to Clojure developers

Fennel is transcoded into Lua using the aniseed plugin.

Lua is the defacto language for configuring Neovim and plugin development and is used where Fennel is not supported.

Although Neovim fully supports Vimscript, this guide will avoid using Vimscript where ever possible.


## Using a REPL Driven Development workflows

Conjure provides the REPL driven development workflow for Clojure (and many other fun languages) and includes a built-in tutorial.

- Vim style Editing
- Starting a REPL (customise startup, add `user` namespace for dev tools)
- Evaluating code
- Structural Editing
- Inspecting data - [portal](https://github.com/djblue/portal)
