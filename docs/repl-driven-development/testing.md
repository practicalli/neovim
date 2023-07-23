# Unit tests and test runners

Run unit tests from within Neovim, showing a summary of test results or a full test report (especially if there are failures)

<!-- TODO: investigate test runner with links in test report to jump to tests / code that is cause of error -->

Or run Kaocka test runners in a terminal session, optionally in watch mode to re-run tests on every saved change.

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

Ensure the `test` directory is included in the classpath when starting a REPL.  Use a project or user-level alias that includes an `:extra-paths` key that includes `["test"]` path

```clojure
clojure -M:env/test:lib/reloaded:repl/rebel
```


## Conjure Test runners

`, t n` to run the tests for the current namespace

![Neovim - Conjure Clojure unit test runner with test results in HUD](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-conjure-tests-results-hud.png)


## External test runner

Open a terminal in Neovim or a separate terminal session to run start a test runner in watch mode.  Tests run automatically when the code changes are saved

Include the `:env/test` alias to include additional paths and dependencies for the test environment configuration, e.g. using additional libraries to run the tests such as mocking or human readable output.

```shell
clojure -X:env/test:test/watch
```

![Kaocha test runner for Clojure in watch mode](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/testing/kaocha-test-runner-watch.png)


!!! HINT "Refine the tests that are watched"
    Start the watcher with [focused or skiped tests by name or meta data (test selectors)](https://cljdoc.org/d/lambdaisland/kaocha/1.66.1034/doc/6-focusing-and-skipping){target=_blank}


Test selectors to run a sub-set of tests based on selector meta data added to `deftest` code

```
clojure -X:test/watch :skip-meta :persistence
```
> TODO: check syntax of Kaocha test selectors

Using Kaocha, specific test namespaces (or specific tests) can be run (or excluded)

```
clojure -X:test/watch :namespace '[practicalli.server"]
```
> TODO: check syntax of Kaocha namespace and specific tests
