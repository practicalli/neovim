# Buffers and Windows

Buffers hold the contents of files and any other information from processes, e.g. the REPL evaluation log

Windows are a container for a buffer and windows can swap which buffer they show.  Multiple windows, also known as splits, can be present in a Neovim frame.  By default, neovim starts with only one window.

A tab can hold one or more windows and tabs can be shown on a tab-line.

## File explorer

Visually manage files with a tree view of the current project, using [:fontawesome-brands-github: Neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim){target=_blank}


=== "Astronvim"
    ++spc++ ++"e"++ toggles neo-tree file browser

    ++spc++ ++"o"++ toggles between buffer and neo-tree

    Neotree icons

    - yellow dot - unsaved changes
    - pencil - git added changes
    - cross - git deleted changes
    - Warning triangle - lsp diagnostics issues

    ++"h"++ ++"j"++ ++"k"++ ++"l"++ to navigate the file tree hierachy

    `<` and `>` to navigate between File, Bufs and Git sources tabs

    ++question-mark++ shows neotree help, listing key bindings


=== "Practicalli Neovim Config Redux"

    ++spc++ ++"f"++ ++"t"++ ++"t"++ to open file explorer


## New File

Files and directories are created in the path given, relative to the directory in which Neovim was opened.

> `:lcd` to set the current local directory
>  
> `:!` for a shell command, e.g. `:!mkdir -p path/to/new/directory` create a new directory and any intermediate path


=== "Astronvim"
    ++spc++ ++"w"++ will write all buffer changes to the associate file.

    ++spc++ ++"n"++ creates a new buffer that can be written to a given file using `:write path/to/filename`

    `:write path/to/filename` will write the current buffer to a new file.

    Use Neotree as a convienient way to create, rename, move and delete files and directories

    ++"a"++ to add a file using the given name, or directory if the name ends in a `/`

    ++"m"++ to move a file or directory

    ++"r"++ to rename a file or directory

    ++"d"++ to delete a file or directory, showing a confirmation prompt first


=== "Practicalli Neovim Config Redux"

    `SPC f b ESC C` to create a new file or directory. The base path is shown in the command bar.  Type the name of directories and file name as required. `RTN` to create or `ESC` to cancel.  The newly created directories or file name appears n the Telescope list and scan be selected for opening.

    !!! HINT "Telescope Normal mode and help"
        `ESC` in Telescope to switch to Normal mode and use comannds, `c` for Create, `r` to rename.
     
        `?` to show all the commands available in Telescope

=== "Neovim"

    `:write path/to/filename` will write the current buffer to a new file

    `:!mkdir path/to/directory` will create a new directory


## Select files and directories

Telescope provides a selector which will narrow the list of matches as a pattern is typed, providing a fast way to find an item in a list.

Telescope provides a preview of the selected file (only if there is sufficient space in the Neovim frame)

File lists are relative to the directory Neovim was opened from (or Path subsequently set in Neovim).

=== "AstroNvim"

    `SPC f f` selector for files within the scope of the current directory path. `SPC f F` to also show hidden files from the current directory path. 
    
    `SPC f a` selector for AstroNvim user configuration files

    `SPC f p` selector for previously opened files (oldfiles)

=== "Practicalli Neovim Config Redux"
    `SPC f f` to list files within the scope of the current directory path.

    `SPC f b` provides a file browser to open files, navigate the file space and create new files and directories


## Buffer management

=== "AstroNvim"

    `SPC f b` selector for currently open buffers

    `SPC b b` to select a buffer from the tab line, pressing the character that appears next to the buffer tab (case sensitive)

    `SPC b D` to delete a buffer from the tab line, pressing the character that appears next to the buffer tab (case sensitive)

    Open multiple buffers when starting Neovim by specifying multiple files to open

    ```bash
    astro README.md deps.edn src/practicalli/playground.clj test/practicalli/playground.clj
    ```

=== "Practicalli Neovim Config Redux"

    `SPC b b` switch between buffers in the current window, using a Telescope popup that lists all current buffers (includes files, Conjure REPL Log, etc.).

    `SPC b n` (`:next`) and `SPC b n` (`:previous`) to cycle through buffers in the current window

    `SPC TAB` (`C-^`) opens the previous buffer, useful to toggle between two buffers in the same window

    Use Telescope to switch between buffers

    ![Neovim - telescope - swtich between buffers](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-telescope-open-buffer.png)

    <!-- TODO: close a buffer (not just its window) -->

    Open multiple buffers when starting Neovim by specifying multiple files to open

    ```bash
    nvim README.md deps.edn src/practicalli/playground.clj test/practicalli/playground.clj
    ```

## Buffer text wrapping

The test in a buffer is not wrapped by default. Set and unset soft text wrapping in a buffer

=== "AstroNvim"
    `SPC u w` toggles wrapping of text

=== "Practicalli Neovim Config Redux"
    line wrap disabled in configuration by default.

    ```fennel title="fnl/config/init.fnl"
    (nvim.ex.set :nowrap)
    ```

=== "Neovim"
    `:set wrap` to set soft wrapping on current buffer

    `:set nowrap` to show lines in full (scroll sideways to see lines longer than the window)


## Window management

Windows can be active (contains the cursor), hidden (open but not shown) or inactive.

=== "AstroNvim"

    `\` creates an horizontal split

    `SPC q` removes the current split


=== "Practicalli Neovim Config Redux"

    `SPC h` / `SPC l` to jump to left / right buffer,  `SPC j` / `SPC k` to jump to buffer below / above
     
    `SPC b b` to list current buffers and switch between them using telescope
     
    `C-w` and `hjkl` to navigate windows is the classic Vim approach


=== "Neovim"
    `C-w` menu to manage Windows, also known as splits.

    `C-w` with one of `hjkl` will move the cursor to the next window in that direction.  Also works with arrow keys.

    `C-w w` toggle between open windows

    `:q` or `C-w q` closes the active window, closing Neovim if it is the last active window.

    > `:wincmd` can be used as an alternative to the Normal mode key bindings


    Open file in a new window

    ```bash
    :sp relative-or-full-filename-path
    ```

    Resize windows

    `C-w` `-`, `+`, `<` or `>` for vertical or horizontal size adjustment


<!-- ## Alt - Arrow keys -->

<!-- Alt+leftarrow will go one window left, etc. -->

<!-- nmap <silent> <A-Up> :wincmd k<CR> -->
<!-- nmap <silent> <A-Down> :wincmd j<CR> -->
<!-- nmap <silent> <A-Left> :wincmd h<CR> -->
<!-- nmap <silent> <A-Right> :wincmd l<CR> -->
