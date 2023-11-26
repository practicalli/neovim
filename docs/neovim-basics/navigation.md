# Navigation

Move the cursor one space at a time 

- ++"h"++ move left
- ++"j"++ move down
- ++"k"++ move up
- ++"l"++ move right


## Jump along line

Move to specific points within a line

- ++"w"++ jump to start of next word
- ++"b"++ jump to start of word
- ++"e"++ jump to end of next word
- ++"$"++ jumps to end of line
- ++"0"++ jumps to start of line
- ++"^"++ jumps to first character of line

!!! HINT "Uppercase w b e consider word delimited by blank characters"
    Jump joined-word using ++"W"++ ++"B"++ ++"E"++ 

Use w b e movement with a number to move the cursor larger distances

```vim title="jump 3 words forward"
3w
```

++"f"++ jumps forward in the current line to the given character

```vim title="jump to next q character"
fq
```

++"F"++ jumps backward in the current line to the given character

```vim title="jump to previous [ character"
F[
```

++"t"++ jumps forward in the current line to before the given character

```vim title="jump before q character"
tq
```

++"T"++ jumps backward in the current line to after the given character

```vim title="jump after [ character"
T[
```


## Jump around buffer

- ++"H"++ jump to top of window
- ++"M"++ jump to middle of window
- ++"L"++ jump to bottom of window
- ++"{"++ jump to previous paragraph
- ++"}"++ jump to next paragraph
- ++"gg"++ jump to first character of line
- ++"G"++ jump to first character of line

Use cursor movement with a number to move the cursor larger distances

```vim title="jump down 12 lines"
12j
```

??? HINT "Relative line numbers for line navigation"
    Enable relative line numbers to show how far away from the current line each other line is.

    ```vim
    set relativenumber
    set number
    ```

    [Practicalli AstroNvim-Config](/neovim/configuration/astronvim/) enables relative line numbers


Jump to a specific line using the number as a command

```vim title="jump to line number"
:127
```

## Jumplist

`:jumps` shows the Neovim jumplist containing all points from any buffer recently jumped to using neovim commands

- ++ctrl++ ++"o"++ jump back 
- ++ctrl++ ++"i"++ jump forward 

## Changes

`:changes` shows the Neovim changelist containing all points in the current buffer which have changed

- ++"g"++ ++semi-colon++ jump back (previous edit)
- ++"g"++ ++full-stop++ jump forward


## Search in buffer

++forward-slash++ searches buffer for the following pattern

- ++"n"++ jumps to next match
- ++"N"++ jumps to previous match

> AstroNvim user config enables `incsearch` incremental search and `hlsearch` to highlight every search match


