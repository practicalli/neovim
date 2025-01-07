# Learning to speak Vim

Learning to speak the language of vim-style editing significantly accelerates the performance of communicating with the computer.

The language is constructed from

- [actions](#actions) to navigate or manipulate text
- [motions](#motions) defining the scope of a cursor movement
- [multipliers](#multipliers) defining the number of times an action or motion takes place
- [text objects](#text-objects) are common scopes within a text document

Actions are coupled with motions or text objects

!!! TIP "keys are mnemonic or regex and have capitalised variants"
    Keys were designed to be mnemonic where possible, e.g. ++"d"++ for delete and  ++"c"++ for change

    Common regular expression scopes are used, e.g. ++0++ first character, ++"$"++ last character

    Keys often have a variant of the action in the capitalised key, e.g. ++shift++ ++"c"++ changes to end of line


## Actions

First learn some verbs, these are your actions:

++"c"++ change

++"d"++ delete

++"g"++ go

++"v"++ visual select

++"y"++ yank (copy)

++"p"++ paste (yanks selected text after pasting), ++"P"++ pastes without yanking

!!! TIP "Double tap to act on current line"
    ++"d"++ ++"d"++ deletes the current line

    ++"y"++ ++"y"++ yanks (copies) the current line


## Motions

Then use those verbs with some motions

++"j"++ ++"k"++ ++"h"++ ++"l"++ move one character down, up, left or right

++"%"++ matching paren `() [] {}` (toggle between open and closed paren)

++grave++ mark character (specify existing mark character)

++open-brace++ ++close-brace++ beginning/end of paragraph

++0++ start of line

++"^"++ first non white-space character of line

++"$"++ end of line

++"a"++ around

++"f"++ find specified character forward, ++"F"++ find backward

++"i"++ inside a range (e.g. a text object like word, or parens)

++"s"++ surround

++"t"++ till (move just before specified character)


## multipliers

An action or motion can be repeated by a given number

++3++ ++"d"++ ++"w"++ deletes the next three words by repeating the action

++"d"++ ++3++ ++"w"++ deletes three words by repeating the motion (follows how this would be said in English)

!!! TIP "Relative line numbers"
    Using relative line numbers an effective way to jump around the visible text of a buffer.

    Each line shows how many lines away it is from the current line.

    ++"j"++ ++"k"++ navigation motions will move down or up the number of lines, e.g. ++1++ ++0++ ++"j"++ will jump down 10 lines.


## Text Objects

Then learn the text objects you can apply verbs and modifiers too

++"b"++ **block/parentheses** a text block or text between parens

++"p"++ **paragraph** text to the next blank line

++"s"++ **sentence** text to a full stop character

++"t"++ **tag** e.g. html/xml tag and its contents

++"w"++ **word** - start of next word, ++"W"++ ignores punctuation


## Examples of speaking Vim

Practice speaking evil with these examples

| Keybinding  | Description                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------|
| ++"c"++ ++"i"++ ++"s"++                           | change inside current sentence (change the whole sentence)            |
| ++"c"++ ++"i"++ ++double-quote++                  | change inside double quotes                                           |
| ++"c"++ ++"f"++ ++")"++                           | change from cursor to next `)` character                              |
| ++"c"++ ++"s"++ ++single-quote++ ++double-quote++ | change by the surrounding single quotes with double quotes            |
| ++"c"++ ++"t"++ ++"X"++                           | change till the character `X` (not including `X`)                     |
| ++"d"++ `/foo`                                    | change until the first search result of ‘foo’                         |
| ++"d"++ ++"d"++                                   | delete current line                                                   |
| ++"D"++                                           | delete current line from cursor onward                                |
| ++"d"++ ++"w"++ ++"w"++                           | delete arround current word (includes trailing space)                 |
| ++"d"++ ++"i"++ ++"w"++                           | delete inside current word (delete word regardless of cusor position) |
| ++"v"++ ++"t"++ ++spc++                           | visual select till the next `Space` character                         |
| ++"v"++ ++"s"++ ++close-bracket++                 | visually select and surround with `[]` without spaces                 |
| ++"v"++ ++"s"++ ++open-bracket++                  | as above with `[ ]` with spaces between parens and content            |
| ++"g"++ ++"v"++                                   | go to last visual selection (select last visual selection)            |
| ++"v"++ ++"a"++ ++"p"++                           | visually select around current paragraph                              |
| ++"v"++ ++"i"++ ++"w"++ ++"S"++ ++double-quote++  | visually select, insert around current word, and surround with quotes |
| ++"y"++ ++"y"++                                   | yank (copy) current line                                              |
| ++"y"++ ++"w"++                                   | yank (copy) current word                                              |
| ++"y"++ ++grave++ ++"y"++                         | yank (copy) to mark `a` (`m a` creates a mark called `a`)             |
