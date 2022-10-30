# Evil Z menu

`z` in normal mode opens a menu of convenient utilities


## Folding code, comments and other content

Code folding is very useful for hiding different levels of detail, for example you could hide everything but the function names in a namespace, showing just the API for that namespace.

Comments and documentation can be folded to help you focus on a specific part of the content.

| Key   | Description                                 |
|-------|---------------------------------------------|
| `z a` | toggle fold of code, comment, section, etc. |
| `z A` | toggle all folds                            |
| `z c` | close fold                                  |
| `z f` | create fold                                 |
| `z M` | close all folds                             |
| `z o` | open fold                                   |
| `z O` | open fold recursive (capital o)             |
| `z r` | fewer folds                                 |
| `z R` | open all folds                              |
| `z x` | update folds                              |

See [narrowing](narrowing.md) for a focused approach to editing.


## Scrolling

Jump the current line to the center, top or bottom of the buffer.

| Key   | Description                                 |
|-------|---------------------------------------------|
| `z b` | scroll the current line to bottom of buffer |
| `z t` | scroll the current line to top of buffer    |
| `z z` | scroll the current line to center of buffer |


## Spelling

`z =` with the cursor on a word shows a list of possible spelling and similar words.

Select a word using its number in tye list to repace the word under the cursor, or `q` to quit the spelling list.

| Key   | Description               |
|-------|---------------------------|
| `z =` | spelling suggestions      |
| `z g` | add word to spelling list |
| `z w` | mark word as misspelled   |

