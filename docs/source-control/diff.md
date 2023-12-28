# Diff

Compare differences between different files or between a file and its versions.

`:diffsplit filename` Neovim command opens a split containing the selected filename, showing a diff comparision to the currently opened file 

> file path completion helps select the correct file for comparison


## nvimdiff

`git difftool` can be configured to use Neovim to show Git diff views of all the files that have changes

!!! EXAMPLE "Configure the Git client to use `nvimdiff` as the `difftool`"
    ```config
    [diff]
      # Neovim diff tool
      tool = nvimdiff
    ```

Run `git difftool` in the root of the project to show the diff of each changed file.

!!! NOTE ""
    ```shell
    git difftool
    ```

++colon++ ++"q"++ ++"a"++ to close the current diff view.  The command line prompts to open the next file as a diff view (assuming there are more files to view).


## Git Diff

DiffView compares working space and staged changes side by side, or a diff for git merge conflicts.

++SPC++ ++"g"++ ++"d"++ or `d` in neogit status buffer (`SPC g s`) will open diffview in a new tab

`q` to return to neogit status buffer

![Neovim diffview plugin - side by side view of changes in git for local working directory and staging](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-neogit-diffview-side-by-side.png)

* Green - added lines
* Yellow - changed line
* Red - deleted lines

=== "AstroNvim"
    ++ctrl++ ++"h"++ / ++"j"++ / ++"k"++ / ++"l"++ to navigate between open splits

=== "Practicalli Neovim Config"
    `SPC b` toggles the sidebar buffer

    `SPC w l` and `SPC w h` to move cursor between diff buffer and sidebar buffer

![Neovim diffview plugin - side by side view of changes in git for local working directory and staging](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-neogit-diffview-side-by-side.png)
