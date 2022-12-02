# Diffview

View working space and staged changes side by side

* Green - added lines
* Yellow - changed line
* Red - deleted lines

`SPC b` toggles the sidebar buffer

`SPC w l` and `SPC w h` to move cursor between diff buffer and sidebar buffer

![Neovim diffview plugin - side by side view of changes in git for local working directory and staging](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-neogit-diffview-side-by-side.png)


## Neogit integration

`d` in neogit status buffer (`SPC g s`) will open diffview in a new tab

`q` to return to neogit status buffer

> [Neogit page](neogit.md) describes diffview integration
