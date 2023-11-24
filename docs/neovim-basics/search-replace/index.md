# Search and Replace

Search and replace within the current buffer:

- use [:fontawesome-solid-book-open: multiple cursors in more detail](../multiple-cursors.md) for in-place editing (visual-multi plugin) 
- `:%substitue` [:fontawesome-solid-book-open: `:substitue` neovim command](substitute.md) for search and replace

Search and replace across a project:

- ++spc++ ++"s"++ ++"s"++ [search and replace commands using Spectre](spectre.md) (AstroNvim community plugin)
- ++spc++ ++"l"++ ++"r"++ to rename symbols using Clojure LSP (AstroNvim) 


## Buffer wide

=== "AstroNvim"
    
    ++"g"++ ++"m"++ ++"A"++ uses visual-multi multiple curses to match all instances of the selected text and in-place editing

    [:fontawesome-solid-book-open: Normal mode editing tools](../multi-modal-editing.md) can be used to replace the text at all cursors simultaneously.

    > [:fontawesome-solid-book-open: multiple cursors in more detail](../multiple-cursors.md) 


=== "Neovim commands"

    Replace all occurances of the current-pattern with the new pattern within the buffer.

    ```vim
    :%s/current-pattern/new-pattern/g
    ```

    Add the `c` option to confirm each replacement

    > Further examples of [:fontawesome-solid-book-open: `:substitue` neovim command](substitue.md)


## Project wide


=== "AstroNvim"


    **Telescope and :cdo**

    ++spc++ ++"f"++ ++"w"++ to search for a word

    ++ctrl++ ++"q"++ opens the quickfix list

    Use `:cdo` command to search and replace in the quickfix list

    ```vim
    :cdo %s/current-pattern/new-pattern/g
    ```

    Including the `c` option to confirm each replacement (using a noice popup when using Practicalli AstroNvim-config)


    **Spectre**

    [:globe_with_meridians: Spectre](https://github.com/nvim-pack/nvim-spectre){target=_blank} is available via the AstroNvim Community project pack and included in the Practicalli astronvim-config    

    ++spc++ ++"s"++ is the search and replace menu

    ![nvim-spectr](https://github.com/windwp/nvim-spectre/wiki/assets/demospectre.gif)

    [:globe_with_meridians: ripgrep](https://github.com/BurntSushi/ripgrep){target=_blank} and [:globe_with_meridians: sed](https://www.gnu.org/software/sed/) are required.

    [:globe_with_meridians: Spectre](https://github.com/nvim-pack/nvim-spectre){target=_blank .md-button}    


=== "Neovim commands"

    !!! WARNING "Evaluating :cdo command as a project wide search replace"
        [:cdo command](https://chrisarcand.com/vims-new-cdo-command/){target=_blank} could be used to search and replace within the results of a tool that finds matching patterns across a project


    ??? INFO "Neovim :help :cdo"
        ```vim
        EXECUTE A COMMAND IN ALL THE BUFFERS IN QUICKFIX OR LOCATION LIST:
        							*:cdo*
        :cdo[!] {cmd}		Execute {cmd} in each valid entry in the quickfix list.
        			It works like doing this:  
        				:cfirst
        				:{cmd}
        				:cnext
        				:{cmd}
        				etc.
         			When the current file can't be |abandon|ed and the [!]
        			is not present, the command fails.
        			When going to the next entry fails execution stops.
        			The last buffer (or where an error occurred) becomes
        			the current buffer.
        			{cmd} can contain '|' to concatenate several commands.

        			Only valid entries in the quickfix list are used.
        			A range can be used to select entries, e.g.:  
        				:10,$cdo cmd
         			To skip entries 1 to 9.

        			Note: While this command is executing, the Syntax
        			autocommand event is disabled by adding it to
        			'eventignore'.  This considerably speeds up editing
        			each buffer.
        			Also see |:bufdo|, |:tabdo|, |:argdo|, |:windo|,
        			|:ldo|, |:cfdo| and |:lfdo|.

        							*:cfdo*
        :cfdo[!] {cmd}		Execute {cmd} in each file in the quickfix list.
        			It works like doing this:  
        				:cfirst
        				:{cmd}
        				:cnfile
        				:{cmd}
        				etc.
         			Otherwise it works the same as `:cdo`.

        							*:ldo*
        :ld[o][!] {cmd}		Execute {cmd} in each valid entry in the location list
        			for the current window.
        			It works like doing this:  
        				:lfirst
        				:{cmd}
        				:lnext
        				:{cmd}
        				etc.
         			Only valid entries in the location list are used.
        			Otherwise it works the same as `:cdo`.

        							*:lfdo*
        :lfdo[!] {cmd}		Execute {cmd} in each file in the location list for
        			the current window.
        			It works like doing this:  
        				:lfirst
        				:{cmd}
        				:lnfile
        				:{cmd}
        				etc.
         			Otherwise it works the same as `:ldo`.
        ```

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
-->
