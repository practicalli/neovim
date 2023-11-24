# Search and Replace

Search and replace within the current line or buffer:

- `g m A` will match text under curor allowing in-place editing with visual-multi plugin 
- `:%substitue` vim-style search and replace (I find this fiddley and not reliable, although could be user errror)

Search and replace across a project:

- Clojure LSP for symbols, etc.


??? HINT "Multiple cursors for multiple substitutions"
    ++"g"++ ++"m"++ ++"A"++ with the cursor on a word will start [multiple cursors](multiple-cursors.md) with a cursor on each occurance.  Vim-editing tools can be used to replace the text at all cursors simultaneously


## Vim Sustitute

`:substitute` or `:s` vim command will highlight the matches for a text pattern and substitute for a new pattern

??? INFO "Built-in help for the command" 
    ```vim
    :help :substitute
    ```

Subsitute the first matching patterns in the current line

```vim
:s/current-pattern/new-pattern
```

Subsitute all the matching patterns in the current line,  `g` representing all occurances in a line

```vim
:s/current-pattern/new-pattern/g
```

Use `%` to specify the current buffer as the scope to change all matches

```vim
:%s/current-pattern/new-pattern/g
```

### Confirm replacement

++"c"++ option at the end prompt for confirmation to replace each occurance

++"y"++ confirms the repacement 


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


[Vims new :cdo command](https://chrisarcand.com/vims-new-cdo-command/)


??? INFO ":help cdo"
    ```help
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
