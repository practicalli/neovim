# Conjure 

![Conjure logo](https://github.com/practicalli/graphic-design/blob/live/logos/conjure-logo-wizard.png?raw=true){align=right loading=lazy style="height:150px;width:150px"}

Conjure is the Clojure REPL client for Neovim.  Code in source code buffers can be evaluated and show the results in-line, providing instant feedback on the behaviour of the code as it develops.

Start a REPL on the command line in the root of a Clojure project.  The REPL should also start an nREPL server for Conjure to connect too.

Conjure will detect the nREPL server when a Clojure file is opended (.clj .edn .cljs .cljc).

=== "Practicalli Clojure CLI Config"
    [:fontawesome-solid-book-open: Practicalli Clojure CLI config](https://practical.li/clojure/clojure-cli/practicalli-config/){target=_blank} contains aliases to  start a REPL process.

    `:repl/rebel` alias starts Rebel rich terminal UI REPL with nREPL server support.  
    
    !!! NOTE ""
        ```shell
        clojure -M:repl/rebel
        ```

    > `clojure -M:repl/basic` starts a REPL with nREPL with a minimal REPL UI
    > 
    > `clojure -M:repl/headless` starts a REPL with nREPL server but without a REPL prompt (to prevent accidental interaction via the command line)

=== "Manual Alias definition"
    Add aliases to the user configuration for Clojure, e.g. `XDG_HOME_CONFIG/clojure/deps.edn` or `HOME/.clojure/deps.edn`
    ```clojure
      ;; Interactive client REPL with nREPL server for Clojure Editor support
      :repl/basic
      {:extra-deps {nrepl/nrepl       {:mvn/version "1.0.0"}
                    cider/cider-nrepl {:mvn/version "0.37.0"}}
       :main-opts  ["--main" "nrepl.cmdline"
                    "--middleware" "[cider.nrepl/cider-middleware]"
                    "--interactive"]}

      ;; Headless REPL with nREPL server for Clojure Editor support
      :repl/headless
      {:extra-deps {nrepl/nrepl       {:mvn/version "1.0.0"}
                    cider/cider-nrepl {:mvn/version "0.37.0"}}
       :main-opts  ["--main" "nrepl.cmdline"
                    "--middleware" "[cider.nrepl/cider-middleware]"]}
    ```
    !!! INFO "Practicalli Clojure CLI Config aliases"
        [:fontawesome-solid-book-open: Practicalli Clojure CLI config](https://practical.li/clojure/clojure-cli/practicalli-config/){target=_blank} defines aliases for a wide range of community tools and libraries that extend the features of Clojure CLI


## Fundamentals

`,eb` to evaluate all the Clojure source code in the current buffer, or `,ef` to evaluate the current function.  The result is displayed inline until the cursor moves.  Open the REPL buffer to see larger results or a complete history.

!!! INFO "Conjure School interative tutorial"
    `:ConjureSchool` runs an interactive tutorial in Neovim, walking through the essential Conjure commands and key bindings 

!!! WARNING "Practicalli Neovim config replaces some key bindings"
    [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux){target=_blank} replaces several key bindings to make them consistent with other Clojure editors


## Evaluation

Clojure REPL workflow encourages code expressions to be evaluated as it is written, providing feedback to ensure expressions are returning the expected results (or to help learn what results a function returns).

`,eb` - evaluate current buffer - used after first starting the REPL to load in a whole namespace and any required namespaces, or to ensure all changes have been evaluated in the REPL

`,ee` - evaluate expression (from start of current form) - especially useful for nested forms

`,ef` - evaluates top-level expression (`,er` is conjure defualt) - most common command

`,ei` - interrupt evaluation (stop long running evaluations) - stop a long running evaluation

`,ew` - evaluate word (symbol) - inspect value of form - i.e. for def names

`,e!` - replace form with its result - helps understand a more complex function by replacing code with a specific value

`,emf` - evaluate marked form - mark forms regularly re-evaluted with `mf` (or any character with `m`) to avoid jumping to that form each time . A capital letter to mark form in a different namespace and evaluate  from the current buffer. 

`"cp` - paste contents of the register into buffer. The result of every evaluation is stored in a Neovim register as well as the log.


## HUD

[practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux){target=_blank} hides the HUD popup.  Practicalli recommends using the REPL log if the inline evaluation results are not sufficient.

If a REPL is running in the current project, then the HUD shows the REPL is connected.

evaluating an expression shows the result in the HUD as well as inline with the code

`,lr` - clear (refresh HUD and keep it visible)


## REPL buffer (log)

The REPL buffer shows a log of the evaluation results for this session and can use more of the available screen than the HUD.

`,ls` - open log in horizontal tab

`,ls` - open log in vertical tab

`,lt` - open log in tab

`,lq` - close log windows (and tabs ??)

`,lr` - soft REPL reset - lead window open

`,lR` - hard REPL reset - close window, delete buffer


## Rich comments

Rich comments are a useful way to contain experimental expressions, or expresisons that should only be evaluated directly by a person developing the code (e.g. starting / stoping services, testing api calls, etc.)

Expressions in rich comments are not included when evaluating the buffer or when expressions are evaluated via a namespace require.

`,ef` to evaluate the top level form within the rich comment, without evaluating the comment expression itself (`,ee` default in Conjure)
