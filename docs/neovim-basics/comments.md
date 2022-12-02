# Comments

[commentary.vim](https://github.com/tpope/vim-commentary) toggles a comment for lines, visual selections or for motions

`gcc` comment current line, `4gcc` comment current line and next 4 lines

`gc` comment region or use with motion e.g. `gcap` comment paragraph,

gc in operator pending mode to target a comment TODO: what is operator pending mode

`:7,17Commentary` comment a range

`:g/TODO/Commentary` as part of a :global invocation

`gcgc` removes comments from a set of adjacent commented lines.
