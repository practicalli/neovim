# REPL Driven Development with Clojure

Conjure provides the REPL driven development workflow for Clojure (and many other fun languages) and includes a built-in tutorial.

- Vim style Editing
- Starting a REPL (customise startup, add `user` namespace for dev tools)
- Evaluating code
- Structural Editing
- Inspecting data - [portal](https://github.com/djblue/portal)

Start a REPL process in a terminal that includes nREPL server.

Conjure will look for the ``.nrepl port in the root of the current project when a Clojure file is opened and connect to the REPL process via that nREPL server.


## Clojure CLI REPL process

Start a rich terminal UI for the Clojure REPL, using Rebel Readline

```
clojure -M:repl/rebel
```

> This guide uses aliases from [`practicalli/clojure-deps-edn`](https://github.com/practicalli/clojure-deps-edn)


Or start a REPL that also includes the `dev` and `test` paths and libraries to hotload dependencies and refresh namespaces, for a reloaded REPL experience.

```
clojure -M:env/dev:env/test:lib/reloaded:repl/rebel
```

> #### Hint::Create a bin/repl script
> Use an executable shell script to save typing the full command line each time, assuming the shell used does not have a useful way to narrow the history (e.g. zsh, fish)
> Create a `bin/repl` file and add the full clojure command to run the REPL process with the required aliases
```shell
#!/usr/bin/env bash
clojure -M:env/dev:env/test:lib/reloaded:repl/rebel
```
