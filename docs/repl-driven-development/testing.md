# Unit tests and test runners

Run unit tests from within Neovim, showing a summary of test results or a full test report (especially if there are failures)

<!-- TODO: investigate test runner with links in test report to jump to tests / code that is cause of error -->

Or run and external test runner via a terminal session, optionally using watch mode to re-run tests on every saved change.

??? INFO "Practicalli sets Kaocha test runner as default"
    [:globe_with_meridians: practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) sets Kaocha as the default test runner

    Kaocha test runner set in [:globe_with_meridians: Astrocommunity Clojure language pack](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/pack/clojure)

    ```lua hl_lines="16" title="Astrocommunity Clojure language pack"
    {
      "Olical/conjure",
      -- load plugin on filetypes
      ft = { "clojure" },
      init = function()
        vim.g["conjure#log#hud#width"] = 1
        vim.g["conjure#log#hud#enabled"] = false
        vim.g["conjure#log#hud#anchor"] = "SE"
        vim.g["conjure#log#botright"] = true
        vim.g["conjure#extract#context_header_lines"] = 100
        vim.g["conjure#eval#comment_prefix"] = ";; "
        vim.g["conjure#client#clojure#nrepl#connection#auto_repl#enabled"] = false
        vim.g["conjure#client#clojure#nrepl#connection#auto_repl#hidden"] = true
        vim.g["conjure#client#clojure#nrepl#connection#auto_repl#cmd"] = nil
        vim.g["conjure#client#clojure#nrepl#eval#auto_require"] = false
        vim.g["conjure#client#clojure#nrepl#test#runner"] = "kaocha"

        vim.api.nvim_create_autocmd("BufNewFile", {
          group = vim.api.nvim_create_augroup("conjure_log_disable_lsp", { clear = true }),
          pattern = { "conjure-log-*" },
          callback = function() vim.diagnostic.disable(0) end,
          desc = "Conjure Log disable LSP diagnostics",
        })
    ```

## Include test path

Ensure the `test` directory is included in the classpath when starting a REPL.  Use a project or user level alias which defines an `:extra-paths` key with the `["test"]` path

!!! NOTE ""
    ```shell
    clojure -M:test/env:repl/reloaded
    ```

## Conjure Test runners

`, t n` to run the tests for the current namespace

`, t a` to run all tests in the project

![Neovim - Conjure Clojure unit test runner with test results in HUD](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-conjure-tests-results-hud.png)


## External test runner

Open a terminal in Neovim or a separate terminal session to run start a test runner in watch mode.  Tests run automatically when the code changes are saved

=== "Practicalli Clojure CLI Config"
    [:fontawesome-solid-book-open: Practicalli Clojure CLI config](https://practical.li/clojure/clojure-cli/practicalli-config/){target=_blank} contains aliases for test runner tools

    - `:test/run` uses Kaocha to run all tests, stopping on first failing test.  Add `:fail-fast? false` argument to run all tests regardless of failure

    - `:test/watch` as above and puts Kaocha in watch mode, triggering a test run each time a file is saved

    Projects created with [Practicalli Project Templates]() include a `test` and `test-watch` task to run Kaocha test runner

    !!! NOTE "Run all tests, stoping on first failing test"
        ```shell
        make test
        ```
    !!! NOTE "Watch for changes and run all tests, stoping on first failing test"
        ```shell
        make test-watch
        ```

    The make tasks call Clojure CLI with the appropriate alias, e.g. `clojure -X:test/run` and `clojure -X:test/watch`

![Kaocha test runner for Clojure in watch mode](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/testing/kaocha-test-runner-watch.png)


## Test Selectors

Use Test selectors to run a sub-set of tests based on selector meta data added to `deftest` code

```clojure
(deftest ^:infrastructure function-name-test
  (testing ""
    (is ,,,))

(deftest ^:persistence function-name-test
  (testing ""
    (is ,,,))
```

=== "Kaocha test runner"
    
    Kaocha test runner can focus or skip on a sub-set of unit tests using test id, metadata, namespaces or a specific deftest. 

    - `:focus` or `:skip` a given namespace or specific test var, i.e. `deftest` 
    - `:focus-meta` or `:skip-meta` test selectors (metadata) on test vars, i.e. `^:persistence`

    Specifying test `:id` in the `tests.edn` configuration file allows different test suites to be run, e.g. `:unit` for unit tests, `:spec` for specification tests 

    Focus and skip works with a single test run or with a continuous watcher.

    !!! EXAMPLE "Skip all tests with :persistence metadata"
        ```shell
        clojure -X:test/watch :skip-meta :persistence
        ```

    !!! EXAMPLE "Focus on a specific test namespace"
        ```shell
        clojure -X:test/watch :focus '["practicalli.gameboard.api.scoreboard-test"]
        ```
       
    !!! EXAMPLE "Focus on a specific unit test (deftest)"
        ```shell
        clojure -X:test/watch :focus '["practicalli.gameboard.api.scoreboard-test/total-score-test"]
        ```
       
    !!! HINT "Refine the tests that are watched"
        Start the watcher with [:globe_with_meridians: focused or skiped tests by name or meta data (test selectors)](https://cljdoc.org/d/lambdaisland/kaocha/1.66.1034/doc/6-focusing-and-skipping){target=_blank}



=== "Cognitect Labs Test Runner"

    [Cognitect Labs Test Runner]() can include or exclude a sub-set of tests, identified by metadata on the var (`deftest`)

    [Cognitect Labs Test Runner - inclusions & exclusions](https://github.com/cognitect-labs/test-runner#using-inclusions-and-exclusions){target=_blank .md-button} 
