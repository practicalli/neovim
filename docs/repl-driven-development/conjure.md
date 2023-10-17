# Conjure

![Conjure logo](https://github.com/practicalli/graphic-design/blob/live/logos/conjure-logo-wizard.png?raw=true){align=right loading=lazy style="height:150px;width:150px"}

Conjure is the Clojure REPL client for Neovim.  Code in source code buffers can be evaluated and show the results in-line, providing instant feedback on the behaviour of the code as it develops.

!!! INFO "Conjure School interative tutorial"
    `:ConjureSchool` runs an interactive tutorial in Neovim, walking through the essential Conjure commands and key bindings. Use the commands provided to move through the guide or ++"j"++ / ++"k"++ to scroll through the guide content.


## Start REPL

Start a REPL on the command line in the root of a Clojure project.  The REPL should also start an nREPL server for Conjure to connect too.

Conjure will detect an nREPL server (via `.nrepl-port` file) when a Clojure file is opended (.clj .edn .cljs .cljc) and connect to the REPL process via that nREPL server.


=== "Practicalli Clojure CLI Config"
    [:fontawesome-solid-book-open: Practicalli Clojure CLI config](https://practical.li/clojure/clojure-cli/practicalli-config/){target=_blank} contains aliases to  start a REPL process that also start an nREPL server.


    Use `repl` make task for projects created by [:fontawesome-solid-book-open: Practicalli Project templates](https://practical.li/clojure/clojure-cli/projects/templates/practicalli/){target=_blank}

    !!! NOTE ""
        ```shell
        make repl
        ```

    Or use the Clojure CLI command with the `:repl/rebel` alias directly

    ```shell
    clojure -M:repl/rebel
    ```

    ??? HINT "Simplify the command line"

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

        [practicalli/dotfiles/Makefile](https://github.com/practicalli/dotfiles/blob/main/Makefile){target=_blank} contains tasks for Clojure development, including running a REPL, preparing dependencies, building an uberjar, lint & format Clojure and configuration files.

        Docker related tasks to build, run and compose common images and containers are also included.


=== "Manual Alias definition"
    Add aliases to the user configuration for Clojure, e.g. `XDG_HOME_CONFIG/clojure/deps.edn` or `HOME/.clojure/deps.edn`
    ```clojure
      ;; Interactive client REPL with nREPL server for Clojure Editor support
      :repl/basic
      {:extra-deps {nrepl/nrepl       {:mvn/version "1.0.0"}
                    cider/cider-nrepl {:mvn/version "0.40.0"}}
       :main-opts  ["--main" "nrepl.cmdline"
                    "--middleware" "[cider.nrepl/cider-middleware]"
                    "--interactive"]}

      ;; Headless REPL with nREPL server for Clojure Editor support
      :repl/headless
      {:extra-deps {nrepl/nrepl       {:mvn/version "1.0.0"}
                    cider/cider-nrepl {:mvn/version "0.40.0"}}
       :main-opts  ["--main" "nrepl.cmdline"
                    "--middleware" "[cider.nrepl/cider-middleware]"]}
    ```
    
    `clojure -M:repl/basic` starts a REPL with nREPL with a minimal REPL UI
     
    `clojure -M:repl/headless` starts a REPL with nREPL server but without a REPL prompt (to prevent accidental interaction via the command line)

    !!! INFO "Practicalli Clojure CLI Config aliases"
        [:fontawesome-solid-book-open: Practicalli Clojure CLI config](https://practical.li/clojure/clojure-cli/practicalli-config/){target=_blank} defines aliases for a wide range of community tools and libraries that extend the features of Clojure CLI


## Evaluation

Clojure REPL workflow encourages code expressions to be evaluated as the are written, providing instant feedback to ensure expected results are returned (or learn the kind of results a function returns).

Results of evaluating an expression are shown in-line.  [Open the REPL log](#repl-log) to see larger results and a complete REPL history for the current session.

`,eb` - evaluate current buffer - used after first starting the REPL to load in a whole namespace and any required namespaces. Use to ensure all changes have been evaluated in the REPL (except those within a `(comment )` form or otherwise commented)

`,er` - evaluate top-level expression (root), ignoring a surrounding `(comment )` form to support the rich comments approach

`,ee` - evaluate expression (from start of current form) - especially useful for nested forms

`,ei` - interrupt evaluation (stop long running evaluations) - stop a long running evaluation

`,ew` - evaluate word (symbol) - inspect value of form - i.e. for def names

`,e!` - replace form with its result - helps understand a more complex function by replacing code with a specific value

`,emf` - evaluate marked form - mark forms regularly re-evaluted with `mf` (or any character with `m`) to avoid jumping to that form each time . A capital letter to mark form in a different namespace and evaluate  from the current buffer. 

`"cp` - paste contents of the register into buffer. The result of every evaluation is stored in a Neovim register as well as the log.


## REPL log

The Conjure REPL log shows the results of every evaluation for the current session.

`,lt` opens log in a new tab page (tab), `,ls` in horizontal split, `,ls` in vertical tab

`,lq` - close log window / tab page

`,lr` - soft REPL reset, leave window open

`,lR` - hard REPL reset, close window & delete buffer

!!! HINT "Inline evaluation over HUD log popup"
    [:fontawesome-solid-book-open: Practicalli Neovim configurations](https://practical.li/neovim/configuration/) hide the HUD log popup that is otherwise shown when Conjure connects to the REPL process, i.e. `vim.g["conjure#log#hud#enabled"] = false`

    In-line evaluation results are the main feedback approach used by Practicalli when evaluating code.

    Practicalli recommends using the REPL log when larger results are returned

    Portal data inspector can be sent evaluation history and provides rich visualisation and navigation tools to explore that history in detail.


## Rich comments

Rich comments are a useful way to contain experimental expressions, or expresisons only evaluated directly by a person developing the code (e.g. starting / stoping services, testing api calls, etc.)

Expressions in rich comments are not included when evaluating the buffer or when expressions are evaluated via a namespace require.

`,er` to evaluate the top level form within the rich comment, without evaluating the comment expression itself.


??? INFO "Start REPL from Neovim"
    Practicalli Configurations require the [:fontawesome-brands-github: vim-jack-in](https://github.com/clojure-vim/vim-jack-in){target=_blank} plugin to be added before this approach will work.

    Start Neovim with a Clojure file, e.g. `nvim src/practialli/playground.clj` or run `nvim` and open a Clojure file, e.g. `*.clj`, `*.cljc`, `*.cljs` or `.edn`.

    * `:Clj` command to start a REPL using Clojure CLI Tools
    * `:Lein` command to start a REPL using Leiningen

    > Neovim switches to a terminal state, use `C-\ C-n` to leave the terminal state.  Use `:N` or `:previous` to switch back to the source code buffer

    `, c f` to connect to the REPL from Conjure, or simply open a Clojure file.  Automated connection will be added in a future version on Conjure.

    > The `vim-jack-in` plugin enables Neovim to call out to Clojure tools or Leiningen to start a REPL and connect to it once its started.

    A full screen REPL log is displayed.  `, l q` to close the log window and return to the Clojure file.
    `, l v` to create a vertical split between code and REPL log, `, l h` for a horizontal split.

