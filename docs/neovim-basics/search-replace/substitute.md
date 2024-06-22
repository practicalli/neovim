# Substitute command

`:substitute` or `:s` command highlights the matches for a text pattern and substitute for a new pattern

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
