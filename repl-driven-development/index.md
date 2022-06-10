# REPL Driven Development with Clojure

Start a REPL process in a terminal that includes nREPL server.

Conjure will look for the .nrepl port in the root of the current project when a Clojure file is opened and connect to the REPL process via that nREPL server.


## Clojure CLI

Start a rich terminal UI for the Clojure REPL, using Rebel Readline

```
clojure -M:repl/rebel
```
 
> This command uses the `:repl/rebel` alias from `practicalli/clojure-deps-edn` 

Or start a REPL that also includes library hotloading and namespace refresh capabilities, for a reloaded REPL experience.

```
clojure -M:lib/reloaded:epl/rebel
```

