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

## Navigate position history

++ctrl+"o" jumps to a previous postion in the cursor history

++ctrl+"i" jumps to a previous postion in the cursor history


## File marks

Navigate within the current file or globally using file marks.

++"m"++ followed by a lower case character creates a mark within the current file.

++"m"++ followed by an upper case character creates a global mark.

++grave++ (backtick) followed by a character jumps to the mark created

++spc++ ++"f"++ ++single-quote++ displays marks in telescope popup

!!! EXAMPLE "File marks within file"
    ++"m"++ ++"f"++ creates a mark lablled `f`

    ++grave++ ++"f"++ jumps to the mark labelled `f`

??? EXAMPLE "Global mark to jump between source and test code"
    ++"m"++ ++"S"++ with the cursor in the source code file.

    ++"m"++ ++"T"++ with the cursor in the test code file.

    ++grave++ ++"S"++ to jump to the source code

    ++grave++ ++"T"++ to jump to the source code

## Jumplist

`:jumps` shows the Neovim jumplist containing all points from any buffer recently jumped to using neovim commands

- ++ctrl++ ++"o"++ jump back 
- ++ctrl++ ++"i"++ jump forward 
- ++"ctrl"++ and navigation key (hjkl) to move to changelist window
- ++"q"++ closes the jumplist buffer


## Changes

`:changes` shows the Neovim changelist containing all points in the current buffer which have changed

- ++"g"++ ++semicolon++ jump back (previous edit)
- ++"g"++ ++period++ jump forward
- ++"ctrl"++ and navigation key (hjkl) to move to changelist window
- ++"q"++ closes the changelist buffer


## Navigation menus

- ++bracket-left++ ++"("++ &  ++bracket-right++ ++")"++ previous & next paren
- ++bracket-left++ ++"brace-left"++ &  ++bracket-right++ ++"brace-right"++ previous and next square brackets
- ++bracket-left++ ++"g"++ &  ++bracket-right++ ++"g"++ previous and next Git hunks
- ++bracket-left++ ++"s"++ &  ++bracket-right++ ++"s"++ previous and next misspelled wor
- d


## Search in buffer

++slash++ searches buffer for the following pattern

- ++"n"++ jumps to next match
- ++"N"++ jumps to previous match

> AstroNvim user config enables `incsearch` incremental search and `hlsearch` to highlight every search match


## Projects

++colon++ ++"c"++ ++"d"++ followed by a path changes the root directory for Neovim.

++tab++ completion simplifies typing the new path of the root directory.

![AstroNvim project root Autocompletion](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-project-change-directory-completion-light.png?raw=true#only-light){loading=lazy}
![AstroNvim project root Autocompletion](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-project-change-directory-completion-dark.png?raw=true#only-dark){loading=lazy}

!!! HINT "AstroNvim rooter"
    AstroNvim has a built-in project root detection utility that updates the current working directory automatically. 

