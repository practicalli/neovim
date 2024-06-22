# Multi-modal Editing

Multi-modal editing has several states optomised for interacting with text

* **normal** - manipulating and navigating existing text (default state)
* **insert** - writing new text
* **visual** - selecting blocks of text

Normal mode to insert mode:

- ++"i"++ insert before the cursor
- ++"a"++ append after the curor
- ++"o"++ insert on new line after current line
- ++"O"++ insert a new line previous to current line

++"v"++ to enter visual select, using navigation and/or motions to select a range.

++esc++ to leave insert or visual mode and return to normal mode.


## Command language

Learn to speak modal editing commands as sentences to effectively learn Multi-modal editing

**Verbs** start the sentence and are the action to perform

- ++"c"++ change
- ++"d"++ delete
- ++"f"++ find character forward
- ++"g"++ go
- ++"s"++ substitute
- ++"v"++ visual select
- ++"y"++ yank (copy)

**Modifiers (motions)** follow verbs and define where the cursor moves to.

- ++single-quote++ a mark location
- ++brace-left++ ++brace-right++ beginning/end of paragraph
- ++"a"++ around
- ++"f"++ find forward (includes character)
- ++"i"++ inside
- ++"S"++ surround (nvim-surround)
- ++"t"++ till (up until)

**Text objects** provide scope for verbs and modifiers

- ++"b"++ block/parentheses
- ++"p"++ paragraph
- ++"s"++ sentence
- ++"t"++ tag, e.g. html/xml tag
- ++"w"++ word
- ++"W"++ word delimited by only space


??? EXAMPLE "Examples of speaking Evil"
    Practice speaking evil with these examples

    | Keybinding  | Description                                                           |
    |-------------|-----------------------------------------------------------------------|
    | `c i s`     | change inside current sentence (change the whole sentence)            |
    | `c i "`     | change inside double quotes                                           |
    | `c f )`     | change from cursor to next `)` character                              |
    | `c s ' "`   | change by the surrounding single quotes with double quotes            |
    | `c t X`     | change till the character `X` (not including `X`)                     |
    | `c /foo`    | change until the first search result of ‘foo’                         |
    | `d d`       | delete current line                                                   |
    | `d i w`     | delete inside the current word (delete word)                          |
    | `v t SPC`   | visual select till the next `Space` character                         |
    | `v s ]`     | visually select and surround with `[]` without spaces                 |
    | `v s [`     | as above with `[ ]` with spaces between parens and content            |
    | `g v`       | go to last visual selection (select last visual selection)            |
    | `v a p`     | visually select around current paragraph                              |
    | `SPC v s "` | visually select current word and surround with `""`                   |
    | `v i w s "` | visually select, insert around current word, and surround with quotes |
    | `y y`       | yank (copy) current line                                              |
    | `y w`       | yank (copy) current word                                              |
    | `y @ a`     | yank (copy) to mark `a` (`m a` creates a mark called `a`)             |


!!! HINT "Evil Reference and Tips"
    [Evil quick reference guide](vim-quick-reference.md)
    [Evil tips for developers](vim-tips-for-developers.md)
    [Speaking Vim](https://stackoverflow.com/questions/1218390/what-is-your-most-productive-shortcut-with-vim/1220118#1220118){target=_blank}

## Selecting text

`vi)` selects all the text within `()`, e.g. (`http://oldwebsite.doh`)


## Surround

`viw` selects the current word, using j/k to modify the selection where required. `o` toggles which end of the selection is expanded/shrunk

`s` substitutes the selection, type the characters to surround the selection.

`p` to paste the original text

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




[Practicalli Spacemacs - Evil reference](https://practical.li/spacemacs/spacemacs-basics/evil/){target=_blank .md-button}
