# Multi-modal Editing

!!! TODO "TODO: Add multi-modal editing in Neovim guide"
    [Practicalli Spacemacs](https://practical.li/spacemacs/spacemacs-basics/evil/) has useful reference content on multi-modal editing (Evil mode).

    Most of this content is the same in Neovim with a few exceptions


## Selecting text 

`vi)` selects all the text within `()`, e.g. `(http://oldwebsite.doh)`


## Surround

`viw` selects the current word, using j/k to modify the selection where required. `o` toggles which end of the selection is expanded/shrunk

`s` substitues the selection, type the characters to surround the selection.

`p` to pase the original text

### nvim-surround

[nvim-surround](https://github.com/kylechui/nvim-surround) provides enhancments over the neovim surround command.

!!! INFO "nvim-surround included in Practicalli AstroNvim Config"

#### Visual Mode

`viw` to select the current word (visual in word)

++"S"++  on a visual selection to surround with next that character, e.g. `S)` to surround with parens.

!!! HINT "Closing paren surrounds without spaces"
    `)`, `]`, `}` surrounds the selected text without spaces between the text and the open and closing parens.

    `(`, `[`, `{` surrounds the selected text with a space between the text and the open and closing parens.

#### Normal mode

`cs` inside an existing pair of characters to change them to another pair of surrounding characters, e.g. `cs(}` to change (text) to {text}

`ds` inside a pair of surrounding characters to delete them, e.g. `ds(` to change (text) to text

`ys` you surround followed by motion and character, e.g. `ysw)` surrounds word with (parens)

`yS` to surround current line

`ySS` to surround current line, placing characters on new lines, e.g. `ySS{` will change "Olical/conjure" to:

```lua
{
    "Olical/conjure"
}
```

The three "core" operations of add/delete/change can be done with the keymaps ys{motion}{char}, ds{char}, and cs{target}{replacement}, respectively. For the following examples, \* will denote the cursor position:

    Old text                    Command         New text
    ----------------------------------------------------
    surr*ound_words             ysiw)           (surround_words)
    *make strings               ys$"            "make strings"
    [delete ar*ound me!]        ds]             delete around me!
    remove <b>HTML t*ags</b>    dst             remove HTML tags
    'change quot*es'            cs'"            "change quotes"
    <b>or tag* types</b>        csth1<CR>       <h1>or tag types</h1>
    delete(functi*on calls)     dsf             function calls

!!! INFO "Neovim help provides details on using nvim-surround"
    ```neovim
    :help nvim-surround.usage
    ```

## Web Links

++"g"++ ++"x"++ on a URL to open in the default browser

## Markdown

`s` in visual mode substitues the selection with the next character typed


`v` to create visual selection, `s` to substitute the current selection, `****` to create a bold style, `P` with the cursor on the second `*` pastes the text that was visually selected. 

### Text style
<!--TODO: add video of manipulating text for markdown -->

`ysiw*` surrounds current word with `*` to create italic text, `.` repeats to make bold text style.

`ds*` removes `*` from current word.


### nvim-surround

nvim-surround plugin assists with adding style characters around text, e.g adding links, italic or bold text, etc.

`S` on a visual selection will surround the text with the next character.  `.` repeat not supported.


**Create a link**

`v` and motion keys to select text, `S [` to surround text with `[]` creating the text of a link anchor.  Use `S (` to surround the URL of the link.

