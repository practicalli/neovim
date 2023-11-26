# Modifying text case

Convert Characters and regioins to upper or lower case text.


## Toggle case with visual select 

`v` to visually select a character or use the vim motion keys to select a region

`U` to uppercase current character or selected region 

`u` to lowercase current character or selected region 

`~` to toggle the case of the text in the selected region

> `.` will repeat the previous selection size and case toggle


## Toggle case menu 

Toggle the current character using vim motion keys, without needing to select a region.

`g ~` opens the toggle case menu

> TODO: Add screenshot of `g ~` toggle case menu

> `g ~ ~` uppercase current line (also works for `RET` and maybe other none-menu characters, but not `SPC`)


## Cheatsheet

- `~` Changes the case of current character
- `guu` Change current line from upper to lower.
- `gUU` Change current LINE from lower to upper.
- `guw` Change to end of current WORD from upper to lower.
- `guaw` Change all of current WORD to lower.
- `gUw` Change to end of current WORD from lower to upper.
- `gUaw` Change all of current WORD to upper.
- `g~~` Invert case to entire line
- `g~w` Invert case to current WORD
- `guG` Change to lowercase until the end of document.
- `gU)` Change until end of sentence to upper case
- `gu}` Change to end of paragraph to lower case
- `gU5j` Change 5 lines below to upper case
- `gu3k` Change 3 lines above to lower case

