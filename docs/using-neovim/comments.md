# Comment lines and regions

Toggle line comment, visual selections or for motions

`gcc` comment current line, `4gcc` comment current line and next 4 lines

`gc` comment region or use with motion e.g. `gcap` comment paragraph,

gc in operator pending mode to target a comment

`:7,17Commentary` comment a range

`:g/TODO/Commentary` as part of a :global invocation

`gcgc` removes comments from a set of adjacent commented lines.


!!! INFO "Operator Pending Mode"
    A state where a command is run after specifying a motion, e.g. `d i w` or `c i )`


## Customise comment pattern

[ts-comments.nvim](https://github.com/folke/ts-comments.nvim){target=_blank} enhances Neovim native comments.

The [default comment for a language](https://github.com/folke/ts-comments.nvim#%EF%B8%8F-configuration){target=_blank} can be modified by specifying a pattern within the `lang = {}` key of the ts-comments.nvim plugin spec.

??? EXAMPLE "Default Clojure comment pattern"
    ```lua
    {
      lang = {
        clojure = { ";; %s", "; %s" },
      },
    }
    ```
