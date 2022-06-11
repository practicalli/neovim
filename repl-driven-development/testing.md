# Unit tests and test runners

Run unit tests from within Neovim, showing a summary of test results or a full test report (especially if there are failures)

<!-- TODO: investigate test runner with links in test report to jump to tests / code that is cause of error -->

Or run Kaocka or Cognitech-Labs test runners in watch mode in a separate terminal session


## Include test path

Ensure the `test` directory is included in the classpath when starting a REPL.  Use a project or user-level alias that includes an `:extra-paths` key that includes `["test"]` path

```clojure
clojure -M:env/test:lib/reloaded:repl/rebel
```


## Conjure Test runners

`, t n` to run the tests for the current namespace

![Neovim - Conjure Clojure unit test runner with test results in HUD](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-conjure-tests-results-hud.png)


<!-- TODO: evaluate neovim test runners and related packages  -->
<!-- - Cognitech Labs -->
<!-- - Kaocha test runner -->
<!-- Are tools like [neotest](https://github.com/nvim-neotest/neotest) - no support for Clojure currently  -->


## External test runner

In a buffer or separate terminal session, start a test runner in watch mode.  Tests run automatically when the code changes are saved

```
clojure -X:test/watch
```

Start the watcher with focused or skiped tests by name or meta data (test selectors)
https://cljdoc.org/d/lambdaisland/kaocha/1.66.1034/doc/6-focusing-and-skipping

For example, specify test selectors to run a sub-set of tests based on selector meta data added to `deftest` code

```
clojure -X:test/watch :skip-meta :persistence
```
> TODO: check syntax of Kaocha test selectors

Using Kaocha, specific test namespaces (or specific tests) can be run (or excluded)

```
clojure -X:test/watch :namespace '[practicalli.server"]
```
> TODO: check syntax of Kaocha namespace and specific tests


## Reference

- [neotest](https://github.com/nvim-neotest/neotest) - Neovim test plugin with some language support (not Clojure - but maybe could be added)
