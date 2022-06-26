# Git and GitHub Version Control

Neogit provides a Magit style client.

> fugitive package provides a command line experience (no keybinding)

`<leader>gs` opens Git Status, by running `:Neogit`

Other commands to map
```
:Neogit kind=<kind> " override kind
:Neogit cwd=<cwd> " override cwd
:Neogit commit" open commit popup
```

## GitHub interaction

Work with GitHub issues and Pull Requests from the comfort of Neovim.

Requires the [GitHub CLI](https://cli.github.com/) for authentication to GitHub, using a developer personal access token that should be added to your GitHub account

TODO: Review [Octo.nvim configuration settings](https://github.com/pwntester/octo.nvim#%EF%B8%8F-configuration)

Command line form: `Octo <object> <action> [arguments]` - [Object, Action and Arguments commands](https://github.com/pwntester/octo.nvim#-commands)

List issues from current project (optionally add a specific repository)
```sh
:Octo issue list
```

Create a pull requests from current project

```sh
:Octo pr create
```

Add a comment to the current topic (issue/pr)
```sh
:Octo comment add

```

```sh
:Octo gist list
```
