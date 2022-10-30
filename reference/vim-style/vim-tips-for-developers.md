# Vim editing for Clojure developers

<!-- TODO: covert from Spacemacs to neovim -->

Vim keybindings that drive Vim editing tools that are common for developers


## Comments and Commenting code

- `g c c`  comment line
- `g c c`  comment line
- `v (select) g c`  comment region
- `g c 9 j`  comment 9 lines from current, downwards


## Simulated structural editing with surround ##

| Keybinding | Description                                                                     |
|------------|---------------------------------------------------------------------------------|
| `v s ]`    | surround with [characters] without spaces                                       |
| `v s [`    | surround with [ characters ] without spaces                                     |
| `c s ( [`  | change surrounding from ( to [                                                  |
| `c i (`    | change in (                                                                     |
| `c a (`    | change “around” (                                                               |
| `%`        | jump forwards to next paren, further `%` toggles between open and close parens. |
| `x p`      | transpose characters (cut current, paste after)                                 |


## Moving around quickly

`f` to jump forward to a given character on the current line. `F` to jump backwards.

`zt`, `zz`, and `zb` to pull the current line to the top/middle/bottom of the screen.

`[number] G` jump to line number or `:22` to jump to line 22

`:7j` to jump 7 lines down

`gf` jump to file name under the cursor - try this in the summary.md file



## Selection, find and replace

`viw` to visual-select in (within) the current word 


## Source code and configuration files

`g D`open definition in another window

`=` (code-aware indenting) operator. Nice with the `ap` (a paragraph) text object.

`C-]` Jump to definition of keyword under the cursor


## code folding

`zc` and `zo` are useful to close and open folds, which can be a nice way of focusing on certain pieces of code.


## Transposing characters and sections ##

`x p`  simple transpose of the current and next character

`M-t` transpose words before and after cursor position

`{`, `}` motions jump to next and previous empty lines.  This motion makes it simple to rearrange paragraphs

`{ d }` will kill the paragraph (or multiple paragraphs)

`{` will jump to the start of the previous paragraph

`p` pastes the killed paragraph before the current paragraph

`>` and `<` (indent and dedent) operators, useful with the aforementioned `}`/`{` motions.



/* ## multi-replace with iedit and narrowing */
