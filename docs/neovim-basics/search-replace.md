# Search and Replace

Search and replace within the current line or buffer:

- `g m A` will match text under curor allowing in-place editing with visual-multi plugin 
- `:%substitue` vim-style search and replace (I find this fiddley and not reliable, although could be user errror)

Search and replace across a project:

- `SPC s` AstroNvim search and replace commands
- Clojure LSP for symbols, etc.


??? HINT "Multiple cursors for multiple substitutions"
    ++"g"++ ++"m"++ ++"A"++ with the cursor on a word will start [multiple cursors](multiple-cursors.md) with a cursor on each occurance.  Vim-editing tools can be used to replace the text at all cursors simultaneously


## Vim Sustitute

`:substitute` or `:s` vim command will highlight the matches for a text pattern and substitute for a new pattern

??? INFO "Neovim :help :substitute" 
    ```vim
    :help :substitute
    ```

Subsitute the first matching patterns in the current line

```vim
:s/current-pattern/new-pattern/
```

> If the new-pattern text is ommitted, then substitute deletes the current-pattern occurances, e.g `:s/current-pattern//`


Subsitute all the matching patterns in the current line,  `g` representing all occurances in a line

```vim
:s/current-pattern/new-pattern/g
```

Use `%` to specify the current buffer as the scope to change all matches

```vim
:%s/current-pattern/new-pattern/g
```

An inclusive line range can be specified to narrow the search

```vim
:4,24s/current-pattern/new-pattern/g
```

`.` can be used to represent the current line of buffer

`$` to represent the last line of the current buffer

```vim
:.,$s/current-pattern/new-pattern/g
```

Match the whole word 


```vim
:.,$s/\<current-pattern\>/new-pattern/g
```

### Substitute history

`:s` and the ++arrow-up++ / ++arrow-down++ will navigate through the substitution history for the current session (from when Neovim was last opened if session was not restored)


### Confirm replacement

++"c"++ option at the end prompt for confirmation to replace each occurance

```vim
:%s/current-pattern/new-pattern/gc
```

++"y"++ confirms the repacement 

++"l"++ confirms the repacement and quits

++"n"++ skips the current occurance and goes to the next one

++"y"++ or ++esc++ to quit substitution


### Regular expression

regular expressions can be used as a search pattern. 

To replace all lines starting with ‘foo’ with ‘NeoVim Rocks’:

```vim
:%s/^foo.*/NeoVim rocks/gc
```

Replace all instances of ‘apple’, ‘orange’, and ‘mango’ with ‘fruit’:

```vim
:%s/apple\|orange\|mango/fruit/g
```

Remove trailing blank space at the end of each line:

```vim
:%s/\s\+$//e
```


## Matching case

`i` option disables the default case sensitive search

```vim
:%s/current-pattern/new-pattern/gi
```

### Visual Select

Use a visual select to search and replace, with confirmation

Note: `'<,'>` is automatically included when in visual mode and `:` is pressed to start a command 

```vim
:'<,'>s/search-text/replace-text/g
```

A potentially more effecitve approach:

- visually select the text
- `*` to select all matching occurances
- `:%s//replace-text/g`



## Project wide

!!! INFO "Evaluating..."

=== "AstroNvim"

    [Spectre](https://github.com/nvim-pack/nvim-spectre){target=_blank} is available via the AstroNvim Community project pack and included in the Practicalli astronvim-config    

    ++spc++ ++"s"++ is the search and replace menu

    [ripgrep](https://github.com/BurntSushi/ripgrep){target=_blank} and [sed](https://www.gnu.org/software/sed/) are required.

    [Spectre](https://github.com/nvim-pack/nvim-spectre){target=_blank .md-button}    


=== "Neovim commands"

[Vims new :cdo command](https://chrisarcand.com/vims-new-cdo-command/){target=_blank .md-button}


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
