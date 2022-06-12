# Buffers and Windows

Buffers hold the contents of files and any other information from processes, e.g. the REPL evaluation log

Windows are a container for a buffer and windows can swap which buffer they show.  Multiple windows, also known as splits, can be present in a Neovim frame.  By default, neovim starts with only one window.


## Buffer management

`SPC f b` opens telescope with a list of the current buffers (includes files, Conjure REPL Log, etc.).  Telescope provides a preview of the selected file

`:next` and `:previous` switch buffers in a window

`C-^` opens the previous buffer, useful to toggle between two buffers in the same window

![Neovim - telescope - swtich between buffers](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-telescope-open-buffer.png)

<!-- TODO: close a buffer (not just its window) -->

Open multiple buffers when starting Neovim by specifying multiple files to open

```bash
nvim README.md deps.edn src/practicalli/playground.clj test/practicalli/playground.clj
```


## Neovim Window management

Windows can be active (contains the cursor), hidden (open but not shown) or inactive.

`C-w` menu to manage Windows, also known as splits.

`C-w` with one of `hjkl` will move the cursor to the next window in that direction.  Also works with arrow keys.

`:q` or `C-w q` closes the active window, closing Neovim if it is the last active window.


> `:wincmd` can be used as an alternative to the Normal mode key bindings
