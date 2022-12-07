# Conjure cheat sheet

Common commands used with Conjure.

!!! HINT "Conjure interactive tutorial"
    `:ClojureSchool` runs an interactive Conjure tutorial in Neovim when Conjure package is installed.


## Evaluation

`,eb` - evaluate current buffer

`,ee` - evaluate expression (from start of current form)

`,ef` - evaluates top-level expression (`,er` is conjure defualt, over-ridden by practicalli/neovim-config-redux)

`,ei` - interrupt evaluation (stop long running evaluations)

`,ew` - evaluate word (symbol) - inspect value of form - i.e. for def names

`,e!` - replace form with its result

`,emf` - evaluate marked form - mark form with mf (or any character with m). Use a capital letter to mark a form in a different namespace / buffer and evaluate if from current buffer

`"cp` - paste contents of the register into buffer. The result of every evaluation is stored in a Neovim register as well as the log.


## HUD

The HUD appears when first opening a Clojure file in Neovim.  If a REPL is running in the current project, then the HUD shows the REPL is connected.

evaluating an expression shows the result in the HUD as well as inline with the code

`,lr` - clear (refresh HUD and keep it visible)


## REPL buffer (log)

`,ls` - open log in horizontal tab

`,ls` - open log in vertical tab

`,lt` - open log in tab

`,lq` - close log windows (and tabs ??)

`,lr` - soft REPL reset - lead window open

`,lR` - hard REPL reset - close window, delete buffer


!!! TODO
    How to switch between log and source code buffer ??


## Rich comments

For expressions in a rich comment, move cursor to top level form within the comment, rather than the comment itself

`,ee` - eval top level form
