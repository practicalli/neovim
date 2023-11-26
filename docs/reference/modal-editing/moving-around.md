# Moving around the cursor

Scrolling is quite inefficient in most editors and moving (jumping) the curor around is far more effective.

Using the `h` `j` `k` `l` as a common part of navigation provides consistency and keeps fingers on the most convienient part of the keyboard.


## Moving by charater

`h` `j` `k` `l` keys move the cursor once character or can be used with numbers to move further.

- `h` move left (often used to move up a path or tree, e.g. a directory path)
- `j` move down
- `k` move up
- `l` move right (often used to move down a path or tree, e.g. a directory path)


## Moving with numbers

`:` followed by a number then one of `h` `j` `k` `l` keys will move the cursor that number in the director of the key.

`3j` will move 3 lines down the buffer (or to the end of the fuffer if there are fewer lines remaining)

Using Relative line numbers showws how far each line is from the current line.  The practicalli/neovim-config sets `:relativenames true` in `fnl/config/init.fnl`.

`42l` moves 42 charaters to the right

> moving by [motions](motions.md) avoids the need to count characters


## Moving around the buffer

`g g` to jump to the top of the current buffer 

`G` to jump to the bottom of the buffer

`z z` moves the current line and cursor to the middle of the window

`z t` moves the current line and cursor to the top of the window

`z t` moves the current line and cursor to the bottom of the window (or as far as the buffer will move in the window)



