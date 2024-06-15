# Spell Check

Neovim has a built-in spell check tool. Grammar checks are not supported.

Incorrect words have a red squiggly underscore.

++"z"++ ++equal++ with the cursor on a word shows a list of possible spelling and similar words.

Select a word using its number in list to replace the word under the cursor, or ++esc++ to close the spelling list.

| Key                        | Description               |
|---------------------------|----------------------------|
| ++"z"++ ++equal++          | spelling suggestions      |
| ++bracket-left++ ++"s"++   | next incorrect word       |
| ++bracket-right++ ++"s"++  | previous incorrect word   |
| ++"z"++ ++"g"++            | add word to spelling list |
| ++"z"++ ++"w"++            | mark word as misspelled   |

