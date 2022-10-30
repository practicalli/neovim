# Neogit - interactive client for Git

Neogit is an interactive git client that provides the core features of version control with Git.  Neogit emulates many of the features found in magit.

`SPC g s` to open `:Neogit` status buffer

`TAB` toggles expansion of sections, files and hunks

`d` provide [a side-by-side view of changes](diffview.md)

`q` to quit Neogit and return to the previous tab

![Neovim Neogit plugin - git status buffer](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-neogit-status.png)

> Neovim is configured to use the magit style key bindings in practicalli/neovim-config-redux


## Branching

`b` opens the branch menu,

* `b` - checkout a branch
* `c` - create a new branch
* `d` - delete a branch, `D` deletes local and remote branch
* `l` - checkout a remote branch and create a local tracking branch
* `m` - rename an existing local branch
* `n` - create a new branch


## Staging changes

`s` to stage change under cursor, either file or hunk. `S` to stage all changes

`u` to unstage change under cursor, `U` to unstage all changes

`v` to select lines to stage within a hunk using `s` or unstage with `u`

## Commit

`c` for the commit menu

`c` for a new commit, `a` to amend the latest commit, `w` to reword a commit message, `e` to add staged changes to existing commit

A new commit or amend commit qill open a new window to write a commit message (using a git commit message template if defined)

`:wq` to save a commit message and initiate the commit.

`:q!`  to cancel the commit from the commit message buffer.


## Stashing changes

`Z` to open the stash menu

`z` to stash the working copy and staged files (index)

`i` to only stash the staged files (index)


## Remote changes

`F` to open the pull menu, `p` to pull changes (fetch and merge) from the remote repository, `u` t pull from the upstream repository, or `e` to specify the remote and branch names.

`P` to open the push menu to open, `-u` to push to the current remote



## Commit history

`L l` to view git commit history log

`RET` on a log entry shows the commit details in a new window (split)

`q` to close the commit details window


## Modify Git commit history

`r` opens the rebase menu

