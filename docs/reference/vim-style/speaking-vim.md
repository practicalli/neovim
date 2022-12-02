# Learning to speak Vim 

Neovim is easier to learn and gain much more benefit from if you learn to speak commands as sentences.

First learn some verbs:

- `c` change 
- `d` delete
- `g` go, 
- `v` visual select 
- `y` yank (copy)

Then use those verbs with some modifiers

- `'` mark 
- `{ }` beginning/end of paragraph
- `0` start of line
- `^` first non white-space character of line
- `$` end of line
- `a` around
- `f` find (includes character)
- `i` inside a range (e.g. word, paren,)
- `s` surround 
- `t` till (move just before specified character)

Then learn the text objects you can apply verbs and modifiers too

- `b` block/parentheses
- `p` paragraph, 
- `s` sentence  
- `t` tag e.g. html/xml 
- `w` word


## Examples of speaking Vim

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
| `D`         | delete current line from cursor onward                                |
| `d i w`     | delete inside the current word (delete word)                          |
| `v t SPC`   | visual select till the next `Space` character                         |
| `v s ]`     | visually select and surround with `[]` without spaces                 |
| `v s [`     | as above with `[ ]` with spaces between parens and content            |
| `g v`       | go to last visual selection (select last visual selection)            |
| `v a p`     | visually select around current paragraph                              |
| `v i w S "` | visually select, insert around current word, and surround with quotes |
| `y y`       | yank (copy) current line                                              |
| `y w`       | yank (copy) current word                                              |
| `y @ a`     | yank (copy) to mark `a` (`m a` creates a mark called `a`)             |

