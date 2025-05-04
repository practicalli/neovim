# Search and Replace

Neovim has several built-in commands to search for patterns in the current buffer and quickfix list can be used to run commands across all the files in a project.

Additional tools that work across all the files in a project:

- ++spc++ ++"s"++ ++"s"++ search and replace using [Grug-far](grug-far.md)
- ++spc++ ++"l"++ ++"r"++ to rename symbols using [Clojure LSP](/neovim/clojure-repl-workflow/refactor-tools/)

> [:fontawesome-solid-book-open: multiple cursors](../multiple-cursors.md) for in-place editing within a buffer


## Buffer search

++slash++ searches through the current buffer, prompting for a pattern to search.

!!! EXAMPLE "Symbol highlight and dot repeat"
    ++"#"++ on a word highlights each occurrence in the buffer, ++"n"++ and ++"N"++ to jump backward and forward for each instance.

    Change the current occurrence (e.g. cw followed by new word)

    Use ++period++ to repeat the change after jumping to the next instance.


### Substitute command

Use the `:substitute` (`:s`) to replace all occurrences of the current-pattern with the new pattern within the buffer.

!!! EXAMPLE "Replace using substitute command"
    ```vim
    :%s/current-pattern/new-pattern/g
    ```

    Add the `c` option to confirm each replacement

 [:fontawesome-solid-book-open: `:substitue` neovim command examples](substitue.md){.md-button}


## Project search and replace

Use search to populate the Neovim quickfix list and change occurrences across all the files in the current project, e.g.:

!!! EXAMPLE "Search word and replace across project using quickfix list"
    ++spc++ ++"f"++ ++"w"++ to search for the supplied word or pattern

    ++ctrl++ ++"q"++ opens the search results in quickfix list

    Use `:cdo` command to search and replace in the quickfix list

    ```vim
    :cdo %s/current-pattern/new-pattern/g
    ```

    Including the `c` option to confirm each replacement


<!-- TODO: review :cdo and similar commands

    use ack.vim/ag.vim with the :cdo command, an intuitive and near-native project-wide find-and-replace solution is now available.

    To replace all instances of foo with bar:

    ```vim
    :Ack foo
    :cdo s/foo/bar/g | update
    ```

    :cdo isn’t the only command that was added around this functionality:

    - :cdo[!] {cmd} - Execute {cmd} in each valid entry in the quickfix list.
    - :cfdo[!] {cmd} - Execute {cmd} in each file in the quickfix list.
    - :ld[o][!] {cmd} - Execute {cmd} in each valid entry in the location list for the current window.
    - :lfdo[!] {cmd} - Execute {cmd} in each file in the location list for the current window.

TODO:
- quickfix list
- `:bufdo`
- `:windo`

-->
