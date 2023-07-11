# Search and Replace

`:substitute` or `:s` vim command will highlight the matches for a text pattern and substitute for a new pattern

Built-in help for the command 

```vim
:help :substitute
```

??? HINT "Multiple cursors can also be used for multiple substitutions"
    [multiple cursors](multiple-cursors.md) created on each occurance can be used to search and replace a pattern


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

