# Files Buffers Windows and Tabs

[Files](#files) are text written to perminant storage, e.g. disk or usb drive and are names with an extension that represents the file type, e.g. `.clj` for clojure, `.md` for markdown, etc.

A [Buffer](#buffers) hold the contents of a file or any other information from processes, e.g. the REPL evaluation log.

[Windows](#windows) are a view on a buffer and windows can swap which buffer they show.  Multiple windows, also known as splits, can be present in a Neovim frame.  

A [tab page](#tab-pages) (or tab) can hold one or more windows and multiple tab pages can be shown on a tab-line. 


## Files

Use [Neo-tree.nvim](#using-neo-tree) to visually navigate and manage files using a tree view of the current project. Files and directories can be added, renamed, moved and deleted.

Use [Telescope](#telescope) to select files, typing a name narrows the file list.


### Using Neo-tree

=== "Astronvim"
    ++spc++ ++"e"++ toggles neo-tree file browser

    ++spc++ ++"o"++ toggles between buffer and neo-tree

    !!! EXAMPLE "Configure hidden files"
        Configure Neotree to display hidden files and directories by default.  They are shown with a different visual style (subtle color) compared to the other files and directories.  

        `H` with the cursor in neotree window will still toggle the display of hidden files and directories.

        Optionally, specify files or directories to never show.
        ```lua title="Practicalli Astronvim-config: plugins/core.lua"
          {
            "nvim-neo-tree/neo-tree.nvim",
            opts = {
              filesystem = {
                filtered_items = {
                  -- when true, they will just be displayed differently than normal items
                  visible = true,
                  -- remains hidden even if visible is toggled to true, this overrides always_show
                  never_show = {
                    ".DS_Store",
                    "thumbs.db",
                  },
                },
              },
            },
          },
        ```

=== "Practicalli Neovim Config Redux"

    ++spc++ ++"f"++ ++"t"++ ++"t"++ to open file explorer

Within Neo-tree:

++"h"++ ++"j"++ ++"k"++ ++"l"++ to navigate the file tree hierachy

++less-than++ and ++greater-than++ to navigate between File, Bufs and Git sources tabs

++question-mark++ shows neotree help, listing key bindings

++"a"++ adds a file, prompting for a name relative to the directory where ++"a"++ was pressed. The name can include new directories to be created. A name ending with ++slash++ will create a directory rather than a file.

++"d"++ deletes the current file or directory (including sub-directories), a conformation prompt is shown

++"r"++ to rename a file or directory (use move to change the path)

++"m"++ to move a file or directory, optionally renaming too

!!! INFO "Neotree icons"
    - yellow dot - unsaved changes
    - pencil - git added changes
    - cross - git deleted changes
    - Warning triangle - lsp diagnostics issues


### Telescope

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



### Save File

Files and directories are created in the path given, relative to the directory in which Neovim was opened.

A file must exist for Neovim to write to it.  Neo-tree and Telescope can be used to create files and directories, as can a terminal and the command line integration (++exclamation++)


=== "Astronvim"
    ++spc++ ++"w"++ will write all buffer changes to the associate file.

    ++spc++ ++"n"++ creates a new buffer that can be written to a given file using `:write path/to/filename`

    `:write path/to/filename` will write the current buffer to a new file.


=== "Practicalli Neovim Config Redux"

    `SPC f b ESC C` to create a new file or directory. The base path is shown in the command bar.  Type the name of directories and file name as required. `RTN` to create or `ESC` to cancel.  The newly created directories or file name appears n the Telescope list and scan be selected for opening.

    !!! HINT "Telescope Normal mode and help"
        `ESC` in Telescope to switch to Normal mode and use comannds, `c` for Create, `r` to rename.
     
        `?` to show all the commands available in Telescope

=== "Neovim"

    `:lcd` to set the current local directory

    `:write path/to/filename` will write the current buffer to a new file

    `:!mkdir path/to/directory` will create a new directory

     If a file is already opened, i.e. with `:edit`, there is some short-hand syntax to simplify the typing

     `:!mkdir -p %:h`

     `-p` option createst any parts of the path required to make the full path

     `%` is the neovim name of the current file

     `:h` for the current directory (the “head” of the path).

     `!` is the NeoVim terminal shell command, e.g. `:!mkdir -p path/to/new/directory` creates a new directory and any intermediate path



### Swap file

Neovim creates a swap file, `.swp`, containing the changes made in a buffer to minimise loss should there be an issue with the computer or Neovim.  Changes are written to the swap file after 200 characters or after 4 seconds pause. 

??? INFO "Swap file location"
    `:swapname` shows the full path to the swap file for the current buffer, e.g. 
    ```shell
    /home/practicalli/.local/state/astronvim/swap//%home%practicalli%projects%practicalli%books%neovim%docs%neovim-basics%files-buffers-windows.md.swp`
    ```

`:preserve` command will write all text from current buffer to the swap file.

`:recover` command overwrites the current buffer with the data from the swap file.  `:recover!` command must be use if the buffer has newer changes than the swap file.  Add a filename after the command to recover to a different file than that contained in the current buffer. 

Opening a file checks if there is an associated swap file and prompts the user 

- (A)bort opening the file
- (D)elete the swap file
- (E)dit anyway, select if the file is newer than the swap file
- (R)ecover the data in the swap file into the file buffer

> `:edit` after the file is open also prompts if there is a swap file.  Selecting (D)elete will delete the swap file without changing the current buffer


## Buffers

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

### Buffer text wrapping

The test in a buffer is not wrapped by default. Set and unset soft text wrapping in a buffer

=== "AstroNvim"
    `SPC u w` toggles wrapping of text

=== "Practicalli Neovim Config Redux"
    line wrap not enabled in configuration by default.

    ```fennel title="fnl/config/init.fnl"
    (nvim.ex.set :nowrap)
    ```

=== "Neovim"
    `:set wrap` to set soft wrapping on current buffer

    `:set nowrap` to show lines in full (scroll sideways to see lines longer than the window)


## Windows 

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


## Tab pages

A Tab page can hold one or more tabs and are useful for grouping different types of files and information. 

A Tab page holds one or more windows, each window is a view on a buffer, a buffer holds the contents of a file or any other information in the editor memory (repl log, etc).

A tab page can provide a logical grouping of windows, e.g. Clojure source code in one tab, tests in a second tab and REPL log in a third.

Neovim window commands may be constrained within the bounds of a tab page (without using the :tab modifier)

Tab pages are often referred to as tabs.


=== "AstroNvim"
    
    ++"g"++ ++tab++ jump to previously selected tab, commonly used to toggle between two tabs  (Practicalli AstroNvim mapping)

    ++"g"++ ++"t"++ jump to next tab page

    ++"g"++ ++"T"++ jump to previous tab page
