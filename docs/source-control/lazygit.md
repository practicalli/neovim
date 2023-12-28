# Lazygit version control

??? INFO "Command Line or AstroNvim configuration"
    Lazygit interface not provided by Practicalli Neovim Config Redux


## Requirements

Install lazygit command line tool


## Open Lazygit

=== "AstroNvim"

    `SPC g g` to open git status with lazygit in a popup window


=== "Command Line"
    Change to the root directory of the git managed project.

    Run the lazygit rich terminal UI

    ```shell
    lazygit
    ```

## Use Lazygit

`SPC` to stage files or directories in the files section of the UI

`c` for a simple commit message prompt in the lazygit UI

`C` to create a commit message within the


!!! INFO "Define Editor for Git Commit Messages"
    Set `core.editor` in the user Git configuration (i.e. `.config/git/config`) to the name of the editor to use for commit messages, e.g. `nvim`, `emacsclient`)
    ```shell title=
    git config --global core.editor = nvim
    ```
    Alternatively, use the `VISUAL` or `EDITOR` environment variable to the choice of editor
