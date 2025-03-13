# Diff

Compare differences between different files or between a file and its versions.

`:diffsplit filename` Neovim command opens a split containing the selected filename, showing a diff comparision to the currently opened file

> file path completion helps select the correct file for comparison


## nvimdiff

The Git `difftool` can specify Neovim as a diff viewer to show Git diff views of all the files that have changes

!!! NOTE "nvimdiff as a command line option"
    ```shell
    git difftool --tool=nvimdiff <optional-filename>
    ```

`git difftool` can be configured to use Neovim

!!! EXAMPLE "Git client config to set `nvimdiff` as `difftool`"
    ```config title="~/.config/git/config"
    [diff]
      # Neovim diff tool
      tool = nvimdiff
    ```

Run `git difftool` in the root of the project to show the diff of each changed file.

!!! NOTE ""
    ```shell
    git difftool <optional-filename>
    ```

++colon++ ++"q"++ ++"a"++ to close the current diff view.  The command line prompts to open the next file as a diff view (assuming there are more files to view).



## DiffView

DiffView compares working space and staged changes side by side, or a diff for git merge conflicts.

++spc++ ++"g"++ ++"d"++ or `d` in neogit status buffer (`SPC g s`) will open diffview in a new tab

++bracket-left++ ++"c"++ to move to previous hunk

++bracket-right++ ++"c"++ to move to next hunk

++spc++ ++"g"++ to return to neovim buffer or ++"q"++ to return to neogit status buffer

++ctrl++ ++"h"++ / ++"j"++ / ++"k"++ / ++"l"++ to navigate between open splits


![Neovim diffview plugin - side by side view of changes in git for local working directory and staging](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-neogit-diffview-side-by-side.png)

* Green - added lines
* Yellow - changed line
* Red - deleted lines
