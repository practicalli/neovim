# Neovim Quick Reference

A reference of the most common keybindings available in Vim Normal mode. [Spacemacs DOCUMENTATION key bindings section](https://github.com/syl20bnr/spacemacs/blob/develop/doc/DOCUMENTATION.org#key-bindings) contains full details

`.` repeats the last keybinding sequence used in Vim Normal mode or a change made within a complete Vim Insert session.

## Moving around

In **Normal** mode you can keep your fingers resting on the main row of your keyboard to move around.

| Key | action                          |
|-----|---------------------------------|
| `j` | move cursor down one line       |
| `k` | move cursor up one line         |
| `l` | move cursor right one character |
| `h` | move cursor left one character  |

In menus such as helm you can move around using `Ctrl` and these keybindings.  So `C-j` will move the cursor down one item in a menu.

### Navigating the current line

| Key | Action                                       |
|-----|----------------------------------------------|
| `f` | to next character (you specify)              |
| `t` | to just before the next character            |
| `;` | repeat `f` or `t` search                     |
| `w` | start of next word                           |
| `W` | start of next word, white space delimited    |
| `e` | end of current word                          |
| `b` | start of previous word                       |
| `W` | end of next word, white space delimited      |
| `*` | to next matching symbol name                 |
| `$` | end of current line                          |
| `0` | start of current line                        |
| `^` | start of non-whitespace                      |
| `%` | jump to matching parens or next closed paren |


### Navigating the current buffer

| Key       | action                                                           |
|-----------|------------------------------------------------------------------|
| `gg`      | start of buffer                                                  |
| `G`       | end of buffer                                                    |
| `H`       | move cursor to head of buffer                                    |
| `M`       | move cursor to middle of buffer                                  |
| `L`       | move cursor to bottom line of buffer                             |
| `C-u`     | jump up half a page                                              |
| `C-d`     | jump down half a page                                            |
| `}`       | move cursor forward by paragraph or block                        |
| `{`       | move cursor backward by paragraph or block                       |
| `ma`      | mark a line in a file with marker "a"                            |
| ``a`      | after moving around, go back to the exact position of marker "a" |
| `'a`      | after moving around, go back to line of marker "a"               |
| `:marks`  | view all the marks                                               |
| `''`      | go to the last place you were                                    |
| `[{`      | jump back to the "{" at the beginning of the current code block  |
| `C-o`     | jump back to previous cursor location (`evil-jump-backwards`)    |
| `C-i`     | Go to newer position in jump list (opposite of `C-o`)            |
| `: 4`     | go to line 4                                                     |



## Text Editing

The following commands put you into the Evil Insert state

| Key | Action                               |
|-----|--------------------------------------|
| `i` | insert state at cursor               |
| `I` | insert state at start of line        |
| `a` | append - insert state after cursor   |
| `A` | append - insert state at end of line |
| `o` | new line after cursor                |
| `O` | new line before cursor               |


## Return to Normal state

Regularly switch back to **normal** state should become common practice.  As soon as you finish typing some new text, it should become second nature to go back to **normal** state.

`ESC` or press `fd` keys in extremely quick succession.


> ####HINT::`fd` shortcut for Esc
> Using `f d` together is low risk as if you dont get it right it will either add the characters or try find the next `d` character (as `f` moves to the next character).
> Keep trying this key combination as once in normal state you can use `u` to undo any `f d` characters inserted.


## Copy, cut, paste, undo, redo

`v` in Vim normal mode changes to Visual select mode.  Use the navigation keys or any other movement keys to select text to copy or cut.

| Key      | Action                                             |
|----------|----------------------------------------------------|
| `y`      | copy (yank) selection and add to kill ring         |
| `x`      | delete character at point and add to kill ring     |
| `X`      | delete character before point and add to kill ring |
| `p`      | paste (put)                                        |
| `u`      | undo                                               |
| `Ctrl-r` | redo                                               |

> ####Hint:: Undo tips
> Undo will revert the last action in normal mode or all the changes you made in **insert** state


## Replace and changing text

| Key            | Action                                  |
|----------------|-----------------------------------------|
| `r`            | replace the character under cursor      |
| `R`            | replace multiple characters until `ESC` |
| `cw`           | change word from cursor to end          |
| `4 c w`        | change 4 words                          |
| `v (select) c` | change region                           |
| `v (select) d` | delete region                           |
| `v i w c`      | change current word                     |
| `v i d`        | delete current word                     |
| `d w`          | delete from cursor to end of word       |
| `C`            | change from cursor to end of line       |
| `D` , `d $`    | delete from cursor to end of line       |


## Delete commands

| Key     | Action                                          |
|---------|-------------------------------------------------|
| `de`    | delete to end of word, not including space      |
| `dw`    | delete to end of word, including space          |
| `d$`    | delete to end of line                           |
| `dd`    | delete the current line                         |
| `4 d w` | delete 4 words                                  |
| `4 d $` | delete 4 lines to end                           |
| `dt`    | delete to a character (not including character) |
| `dab`   | delete a whole block / expression               |
| `dib`   | delete contents of a block / expression         |
| `cab`   | change all the block / expression               |
| `cib`   | change inner block contents / expression        |
| `yab`   | yank all block / expression                     |
| `yib`   | yank inner block contents / expression          |



## Repeat commands

| Key              | Action                           |
|------------------|----------------------------------|
| `.`              | repeat last command again        |
| `<number> <cmd>` | repeat command a number of times |

The `.` keybinding will repeat the last command in normal mode or the last text edit in insert mode.

Type a number before a command and that command will run that number of times.

>####Hint::Inserting a comment border
> Use the number repeat to create a border of 42 `;` characters.
> Type `42` to repeat the command 42 times
> Press `i` for insert mode
> Press `;` as the character to repeat insert
> Press `ESC` or `fd` to leave insert mode and insert all 42 `;` characters


## Transposing / swap

| Key    | Description                                                 |
|--------|-------------------------------------------------------------|
| `x p`  | transpose the current character with the next character     |



## Comments - works for all major modes

`g c c` to comment out the current line

`g c` to comment out the currently selected region

To comment multiple lines you can use the repeat command style, especially useful if you are using relative line numbers.

`g c 3 j` will comment the current line and the following two lines below.  Comment in reverse using `g c 3 k`.

In Visual state, `v`, select the lines you wish to comment and use `g c` to comment all the marked lines.  Partially marked lines are not commented.


## Managing Files

Files in practicalli/neovim-config can be managed with Telescope plugin, although the neovim commands can also be used

`SPC p t` toggles a visual file explorer on as a leftmost window, providing a further way to navigate files and directories.

| Key             | Description                                          |
|-----------------|------------------------------------------------------|
| `SPC f f`       | find existing file (from current local root of neovim) |
| `SPC f /`       | copy file - save current buffer with a new file name |
| `SPC f b`       | browse files - `Esc` to run commands                 |
| `SPC f b Esc r` | change file name of current buffer                   |

Telescope file browser opens in **Insert** mode to allow typing filenames, to narrow the results in the Telescope popup.

### Telescope browser commands

`SPC f b` opens telescope browser which allows commands to be run over the current file or directory.

`Esc` swiches the Telescope popup to normal mode, allowing commands to be used

- `c` create file / directory  (any missing parts of a path are created)
- `r` rename a file / directory 
- `R` replace

`TAB` selects files and directories, allowing for commands (i.e. rename) to be done in batch mode (acting on all selected files / directories)


## Working with Buffers

To work with files in Neovim they are loaded into a **Buffer**.

Buffers are displayed in a window and you can change the window to show any of the current buffers.

`SPC b` displays the buffer menu and the most common commands include:

| Key       | Command            | Description               |
|-----------|--------------------|---------------------------|
| `SPC b b` | :Telescope buffers | List current buffers      |
| `SPC b d` | :bdelete           | Kill current buffer       |
| `SPC b n` | :bnext             | Switch to next buffer     |
| `SPC b p` | :bprevious         | Switch to previous buffer |
| `SPC b a` | :ball              | Switch to previous buffer |



## Quit or Restart Emacs

I recommend using the Spacemacs menu from **normal** mode to quit / restart Spacemacs.

| Key       | Action                                             |
|-----------|----------------------------------------------------|
| `SPC q a` | Quit Neovim (blocked if unsaved change in buffers) |
| `SPC q q` | Quit buffer (blocked if unsaved change in buffers) |
| `SPS q Q` | Force quit of Neovim                               |



### External commands

run external commands using `:!` followed by a command.  For example:

`:!ls` - run the `ls` command


