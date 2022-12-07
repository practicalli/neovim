# Octo - GitHub issues and PRs

Octo issues and pull requests to be created, updated and deleted from within Neovim.


## GitHub interaction

[GitHub CLI](https://cli.github.com/){target=_blank .md-button}

Work with GitHub issues and Pull Requests from the comfort of Neovim.

[GitHub CLI](https://cli.github.com/){target=_blank} to authentication to a GitHub account.  Successful login creates a local developer token that is used by Octo to communicate with GitHub.

```shell
gh auth login
```

### Octo commands

Command line form: `Octo <object> <action> [arguments]` - [Object, Action and Arguments commands](https://github.com/pwntester/octo.nvim#-commands){target=_blank}

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

!!! HINT "Octo.nvim configuration options"
    [Octo.nvim configuration options](https://github.com/pwntester/octo.nvim#%EF%B8%8F-configuration){target=_blank}
