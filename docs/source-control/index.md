# Version Control

There are several ways to interact with Git version control, although Practicalli recommends Neogit interactive git client and Octo to manage GitHub issues and pull requests

- [lazygit](lazygit.md) terminal UI (requires lazygit cli tool)
- [Neogit](neogit.md) rich git client (similar to Emacs Magit), with Diffview integration
- [Octo](octo.md) for GitHub Issue and Pull Requests
- [Open in GitHub](open-in-github.md)
- Shell out to the command line, `:!`
- Git commands in Neovim terminal buffer


## Common Git actions

### Initialise local repository"

++spc++ ++"t"++ ++"f"++ opens floating terminal window in the current root directory root (use `:cd` to change the root directory).

```shell
git init .
```

### Stage change in buffer

The current hunk or the whole buffer can be staged from the buffer using Git Signs, saving a trip to the Git Status buffer.

++spc++ ++"g"++ ++"H"++ stages the current hunk

++spc++ ++"g"++ ++"S"++ stages the current buffer


### Git Status

`SPC g g` opens lazygit status, for minimal UI

![AstroNvim Git - Lazygit status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-git-lazygit-status-example-light.png?raw=true#only-light){loading=lazy}
![AstroNvim Git - Lazygit status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-git-lazygit-status-example-dark.png?raw=true#only-dark){loading=lazy}

++spc++ ++"g"++ ++"s"++  ++spc++ ++"g"++ ++"n"++ ++"t" opens neogit in a new tab for Magit style experience


![Neovim Neogit plugin - git status buffer](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-neogit-status.png)


## GitHub Issues & Pull Requests

Interact with the remote GitHub repository using [Octo](octo.md)

List issues from a specific repository

```shell
:Octo issue list practicalli/neovim
```

![Neovim Octo GitHub Issues list for practicalli/neovim](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-octo-github-issue-list.png)


Create a pull request on a specific repository

```shell
:Octo pr create practicalli/neovim
```
