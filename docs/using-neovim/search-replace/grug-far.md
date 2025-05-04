# Grug Far

A very efficient search and replace tool using the external [ripgrep command](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md) line tool.

++spc++ ++"s"++ is the search and replace menu

++"g"++ ++"?"++ for help menu in the Grug-far buffer


!!! NOTE "Search and replace with Grug-Far"

    ++spc++ ++"s"++ ++"s"++ to search across the current workspace (project)

    Enter a Search pattern, press ++esc++ and all occurrences across the project are shown

    Enter a Replace pattern, press ++esc++ to see occurrences with their replacement

    ++comma++ ++"r"++ to replace all occurrences with the replace pattern

    ++comma++ ++"j"++ / ++"k"++ replace at current line & move to next / previous change



??? TIP "Search results in Quicklist"
    ++comma++ ++"q"++ adds search results to quickfix list to edit occurrences with other Neovim tools


## Search buffer

Enter patterns in the **Search** and **Replace** and the results are show in a diff below.

++tab++ and ++shift++ ++tab++ navigate between search buffer sections.

![Grug-Far Search buffer](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim-5/neovim-search-grug-far-search-dark.png?raw=true){loading=lazy}

??? EXAMPLE "Usefull Ripgrep options for Grug-Far"
    - `-i/--ignore-case`: ignore case differences, e.g. `rg -i fast` matches `fast`, `fASt`, `FAST`, etc.
    - `-F/--fixed-strings`: Disable regular expression matching and treat the pattern as a literal string.
    - `-w/--word-regexp`: pattern matches are surrounded by word boundaries, e.g. `pattern` is `\b(?:pattern)\b`.
    - `-c/--count`: a count of total matched lines.
    - `-a/--text`: Search binary files as if they were plain text.
    - `-U/--multiline`: Permit matches to span multiple lines.
    - `-z/--search-zip`: Search compressed files (gzip, bzip2, lzma, xz, lz4, brotli, zstd). This is disabled by default.
    - `-C/--context`: Show the lines surrounding a match.
    - `-L/--follow`: Follow symbolic links while recursively searching.
    - `-M/--max-columns`: Limit the length of lines printed by ripgrep.

    [All Ripgrep Options](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#common-options)
