# Version Control

There are several ways to interact with Git version control, although Practicalli recommends Neogit interactive git client and Octo to manage GitHub issues and pull requests

* [Neogit](neogit.md) git client (similar to Emacs Magit)
* [Octo](octo.md) for GitHub Issue and Pull Requests
* [Diffview](diffview.md)

> Shell out to command line or the Neovim terminal buffer to run git commands directly


## Overview

`SPC g s` opens Git Status tab, by running `:Neogit`

![Neovim Neogit plugin - git status buffer](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-neogit-status.png)


`d` in neogit status buffer (`SPC g s`) will open diffview in a new tab

![Neovim diffview plugin - side by side view of changes in git for local working directory and staging](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-neogit-diffview-side-by-side.png)


List issues from current project (optionally add a specific repository)

```sh
:Octo issue list practicalli/neovim
```

![Neovim Octo GitHub Issues list for practicalli/neovim](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-octo-github-issue-list.png)
