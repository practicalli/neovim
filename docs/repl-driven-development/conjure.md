# Conjure cheatsheet

## Evaluation

`,eb` - evaluate current buffer

`,ee` - evaluate expression (from start of current form)

,ef -

`,ei` - interrupt evaluation (stop long running evaluations)

`,ew` - evaluate word (symbol) - inspect value of form - i.e. for def names

,e! - replace form with its result 

,emf - evaluate marked form - mark form with mf (or any character with m) 
- Use a capital letter to mark a form in a different namespace / buffer and evaluate if from current buffer

;; The result of every evaluation is stored in a Neovim register as well as the log.                                                                                                                        
"cp - paste contents of the register into buffer


## HUD  

The HUD appears when first opening a Clojure file in Neovim.  If a REPL is running in the current project, then the HUD shows the REPL is connected.

evaluating an expression shows the result in the HUD as well as inline with the code

`,lr` - clear (refresh HUD and keep it visible)

## REPL buffer (log)                                                                                                                                                                                                            

,ls - open horizontal

,ls - open vertical

,lt - open in tab

,lr - soft reset - lead window open

,lR - hard reset - close window, delete buffer 

,lq - close log windows (and tabs ??)                                                                                                                                                                 
                                                                                                                                                                                                            
?? How to switch between log and source code buffer ??                                                                                                          
                                                                                                                                                                                                                                                                           
                                                 
## Rich comments                                                          

for expressions in a rich comment, move cursor to top level form within the comment, rather than the comment itself

,ee - eval top level form 


