# Using Newovim

Using the fundamental controls of Neovim that apply across any and all editing.

![Neovim startup with dashboard theme](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-startup-dashboard-theme-light.png)


## Managing files and directories

`SPC f p` to list files within the scope of the current directory path. `SPC f f` to open a file browser which can open, create and delete files and directories.

`:lcd` to set the current local directory

`:!` for a shell command, e.g. `:!mkdir -p path/to/new/directory` create a new directory and any intermediate path



## Manage buffers and windows

`SPC h` / `SPC l` to jump to left / right buffer,  `SPC j` / `SPC k` to jump to buffer below / above

`SPC b b` to list current buffers and switch between them using telescope

`C-w` and `hjkl` to navigate windows is the classic Vim approach
