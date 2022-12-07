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

[GitHub CLI](https://cli.github.com/){target=_blank .md-button}

Work with GitHub issues and Pull Requests from the comfort of Neovim.

[GitHub CLI](https://cli.github.com/){target=_blank} to authentication to a GitHub account.  Successful login creates a local developer token that is used by Octo to communicate with GitHub.

```shell
gh auth login
```

![GitHub CLI authorization login wizzard](https://raw.githubusercontent.com/practicalli/graphic-design/live/git/github-cli-auth-login-wizzard.png)


### Octo commands

Command line form: `Octo <object> <action> [arguments]` - [Object, Action and Arguments commands](https://github.com/pwntester/octo.nvim#-commands){target=_blank}

List all repositories owned by the GitHub authenticated user

```shell
:Octo repo list
```

List issues from current project (optionally add a specific repository)
```sh
:Octo issue list practicalli/neovim
```

> The account/repository-name is required if Octo cannot find the repository


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

![Neovim Octo package - GitHub Gist list](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-octo-github-gist-list.png)


!!! HINT "Octo.nvim configuration options"
    [Octo.nvim configuration options](https://github.com/pwntester/octo.nvim#%EF%B8%8F-configuration){target=_blank}
