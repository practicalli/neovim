# REPL Driven Development with Clojure

Conjure provides the REPL driven development workflow for Clojure (and many other fun languages) and includes a built-in tutorial.

- Vim style Editing
- Starting a REPL (customise startup, add `user` namespace for dev tools)
- Evaluating code
- Structural Editing
- Inspecting data - [portal](https://github.com/djblue/portal){target=_blank}

Start a REPL process in a terminal that includes nREPL server.

Conjure will look for the ``.nrepl port in the root of the current project when a Clojure file is opened and connect to the REPL process via that nREPL server.


## Clojure CLI REPL process

Start a rich terminal UI for the Clojure REPL, using Rebel Readline

```
clojure -M:repl/rebel
```

> This guide uses aliases from [`practicalli/clojure-deps-edn`](https://github.com/practicalli/clojure-deps-edn){target=_blank}


Or start a REPL that also includes the `dev` and `test` paths and libraries to hotload dependencies and refresh namespaces, for a reloaded REPL experience.

```
clojure -M:env/dev:env/test:lib/reloaded:repl/rebel
```

## Simplify the command line

Add [a `Makefile` to define common tasks to simplify and add consistency to working with Clojure across projects](https://practical.li/blog/posts/make-clojure-tasks-simple-and-consistent/){target=_blank}  or shell script to simplify the commands used to call `clojure` to run common tasks

```Makefile
repl:  ## Run Clojure REPL with rich terminal UI (Rebel Readline)
    $(info --------- Run Rebel REPL ---------)
    clojure -M:env/dev:env/test:repl/rebel


repl-reloaded:  ## Run Clojure REPL with hotload, reload and rich terminal UI (Rebel Readline)
    $(info --------- Run Rebel REPL ---------)
    clojure -M:env/dev:env/test:lib/reloaded:repl/rebel
```

A `Makefile` can also include supporting commands, such as lint and format tools.

```Makefile
# Run MegaLinter with custom configuration
lint:
    $(info --------- MegaLinter Runner ---------)
    mega-linter-runner --flavor java --env 'MEGALINTER_CONFIG=.github/linters/mega-linter.yml'
```

!!! HINT "Practicalli Makefile"
    [practicalli/dotfiles/Makefile](https://github.com/practicalli/dotfiles/blob/main/Makefile){target=_blank} contains tasks for Clojure development, including running a REPL, preparing dependencies, building an uberjar, lint & format Clojure and configuration files.

    Docker related tasks to build, run and compose common images and containers are also included.

## References

* [Which Clojure CLI execution option - M T X P - should be used](https://practical.li/blog/posts/clojure-which-execution-option-to-use/)
* [Using a Makefile to simplify Clojure development tasks](https://practical.li/blog/posts/make-clojure-tasks-simple-and-consistent/)
