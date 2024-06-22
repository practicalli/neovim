# Files Buffers Windows and Tabs

[Files](#files) are text written to perminant storage, e.g. disk or usb drive and are names with an extension that represents the file type, e.g. `.clj` for clojure, `.md` for markdown, etc.

A [Buffer](#buffers) hold the contents of a file or any other information from processes, e.g. the REPL evaluation log.

[Windows](#windows) are a view on a buffer and windows can swap which buffer they show.  Multiple windows, also known as splits, can be present in a Neovim frame.

A [tab page](#tab-pages) (or tab) can hold one or more windows and multiple tab pages can be shown on a tab-line.


## Files

`SPC e` opens [Neo-tree.nvim](#using-neo-tree) which shows a visual tree to navigate and manage files from the current project (root). Files and directories can be added, renamed, moved and deleted.

++spc++ ++"f"++ ++"f"++ to find files with [Telescope](#telescope), typing a pattern narrows the selectable file list.

!!! HINT "Set root directory in Neovim"
    All file commands respect the currently set directory root for Neovim.

    The root is set to the current directory when opening a file.

    `:cd ~/new/directory/path` will change the current root to the new path.

    ++period++ in Neotree sets the root to the current directory (parent directory if on a file)

### Using Neo-tree

++spc++ ++"e"++ toggles neo-tree file browser

++spc++ ++"o"++ toggles between buffer and neo-tree

++enter++ in Neo-tree opens the current file in a buffer



### Key bindings Within Neo-tree

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


??? EXAMPLE "Configure hidden files"
    Configure Neotree to display hidden files and directories by default.  They are shown with a different visual style (subtle color) compared to the other files and directories.

    `H` with the cursor in neotree window will still toggle the display of hidden files and directories.

    Optionally, specify files or directories to never show.
    ```lua title="lua/plugins/neo-tree.lua"
    ---@type LazySpec
    return {
      "nvim-neo-tree/neo-tree.nvim",
      config = function()
        require("neo-tree").setup {
          filesystem = {
            filtered_items = {
              visible = true, -- show hidden files in alternate style
              hide_dotfiles = true,
              hide_gitignored = true,
              hide_hidden = true, -- only works on Windows for hidden files/directories
              hide_by_name = {
                --"node_modules"
              },
              hide_by_pattern = { -- uses glob style patterns
                --"*.meta",
                --"*/src/*/tsconfig.json",
              },
              always_show = { -- remains visible even if other settings would normally hide it
                --".gitignored",
              },
              never_show = { -- remains hidden even if visible is toggled to true, this overrides always_show
                --".DS_Store",
                --"thumbs.db"
              },
              never_show_by_pattern = { -- uses glob style patterns
                --".null-ls_*",
              },
            },
          },
        }
      end,
    }
    ```

### Telescope

Telescope provides a selector which will narrow the list of matches as a pattern is typed, providing a fast way to find an item in a list.

Telescope provides a preview of the selected file (only if there is sufficient space in the Neovim frame)

File lists are relative to the directory Neovim was opened from (or Path subsequently set in Neovim).

`SPC f f` selector for files within the scope of the current directory path. `SPC f F` to also show hidden files from the current directory path.

`SPC f a` selector for AstroNvim user configuration files

`SPC f p` selector for previously opened files (oldfiles)


### Save File

Files and directories are created in the path given, relative to the directory in which Neovim was opened.

A file must exist for Neovim to write to it.  Neo-tree and Telescope can be used to create files and directories, as can a terminal and the command line integration (++exclamation++)

++spc++ ++"w"++ will write all buffer changes to the associate file.

++spc++ ++"n"++ creates a new buffer that can be written to a given file using `:write path/to/filename`

++spc++ ++"W"++ was added to Practicalli Astro Config as a key binding for `:write path/to/filename` which writes the current buffer to a new file, prompting for the file name.

!!! HINT "Telescope Normal mode and help"
    `ESC` in Telescope to switch to Normal mode and use comannds, `c` for Create, `r` to rename.

    `?` to show all the commands available in Telescope


### Path commands

`:lcd` to set the current local directory

`:write path/to/filename` will write the current buffer to a new file

`:!mkdir path/to/directory` will create a new directory

If a file is already opened, i.e. with `:edit`, there is some short-hand syntax to simplify the typing

```command
:!mkdir -p %:h
```

`-p` option creates any parts of the path required to make the full path

`%` is the neovim name of the current file

`:h` for the current directory (the “head” of the path).

`!` is the NeoVim terminal shell command, e.g. `:!mkdir -p path/to/new/directory` creates a new directory and any intermediate path


### Directories

++"a"++ in Neotree to create a file or by adding a ++forward-slash++ at the end of the name a directory is created.

Use the `mkdir` shell command to create a new directory, which is created relative to the current path, which can be checked with `:lcd`

`:!mkdir full/path/to/new/directory`

If a file is already opened, i.e. with `:edit`, there is some short-hand syntax to simplify the typing

```shell
:!mkdir -p %:h
```

`mkdir -p` - the UNIX command to create a folder, the `-p` option creating any parts of the path required to make the full path

`%` - name of the current file

`:h` - for the current directory (the “head” of the path).

`!` - the NeoVim terminal shell command


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

`SPC f b` selector for currently open buffers

`SPC b b` to select a buffer from the tab line, pressing the character that appears next to the buffer tab (case sensitive)

`SPC b D` to delete a buffer from the tab line, pressing the character that appears next to the buffer tab (case sensitive)

Open multiple buffers when starting Neovim by specifying multiple files to open

```bash
astro README.md deps.edn src/practicalli/playground.clj test/practicalli/playground.clj
```

!!! HINT "Open multiple buffers at starup"
    Open multiple buffers when starting Neovim by specifying multiple files to open

    ```shell
    astro README.md deps.edn src/practicalli/playground.clj test/practicalli/playground.clj
    ```

### Buffer text wrapping

The test in a buffer is not wrapped by default. Set and unset soft text wrapping in a buffer

++spc++ ++"u"++ `SPC u w` toggles wrapping of text


## Windows

Windows can be active (contains the cursor), hidden (open but not shown) or inactive.

`\` creates an horizontal split

`SPC q` removes the current split


??? INFO "Neovim commands"
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


## Tab pages

A Tab page can hold one or more tabs and are useful for grouping different types of files and information.

A Tab page holds one or more windows, each window is a view on a buffer, a buffer holds the contents of a file or any other information in the editor memory (repl log, etc).

A tab page can provide a logical grouping of windows, e.g. Clojure source code in one tab, tests in a second tab and REPL log in a third.

Neovim window commands may be constrained within the bounds of a tab page (without using the :tab modifier)

Tab pages are often referred to as tabs.

++"g"++ ++tab++ jump to previously selected tab, commonly used to toggle between two tabs  (Practicalli AstroNvim mapping)

++"g"++ ++"t"++ jump to next tab page

++"g"++ ++"T"++ jump to previous tab page
