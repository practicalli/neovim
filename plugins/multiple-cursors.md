# Multiple cursors

[Visual-Multi (VM)](https://github.com/mg979/vim-visual-multi) is a multiple selections/cursors plugin that uses modal editing and provide visual feedback when editing multiple lines simultaneously.

Mulitple cursors is generally useful when editing smilarly structured lines with diffferent content.  Cursors are moved by column position or by using vim motions.

`\ \ c` creates a cursor at the start of every visual selection line

`\ \ \` toggle cursor at position 


## Command quick reference    
 
`\ \` is the leader for multiple cursors and will show the visual-multi menu in which-key.  

These commands cover the large majority of use cases for multiple cursors.

> `:help g:VM_maps` for a reference of all mappings and instructions on how to change them

<!-- TODO: How to define the visuual-multi leader key in fennel  
    let g:VM_leader = '\'
-->
 
| Action                        | Key         | Command              |
|-------------------------------|-------------|----------------------|
| Add Cursor at Position        | `\\\`       | `vm-add-cursor`      |
| Alignm VM cursors with cursor | `\\a`       | `vm-align`           |
| Select All Words              | `\\A`       | `vm-select-all`      |
| Transposition                 | `\\t`       | `vm-transpose`       |
| Toggle Mappings               | `\\<Space>` | `vm-mappings-toggle` |
| Find with Regex               | `\\/`       | `vm-regex-search`    |
| Reselect Last                 | `\\gS`      | `vm-reselect-last`   |

Once visual-multi has started the vm-mappings-buffer mappings are available:

| Action              | Key                     | Command            |
|---------------------|-------------------------|--------------------|
| Find Word           | `<C-n>`                 | vm-find-word       |
| Next/Previous/Skip  | `n` / `N` / `q`         | vm-find-next       |
| Remove Region       | `Q`                     | vm-remove-region   |
| Add Cursors Down/Up | `<C-Down>` / `<C-Up>`   | vm-add-cursors     |
| Select Right/Left   | `<S-Right>`, `<S-Left>` | vm-shift-select    |
| Slash motion        | `g/`                    | vm-slash           |
| Select Operator     | `s`                     | vm-select-operator |
| Find Operator       | `m`                     | vm-find-operator   |


> NOTE: `C-n` conflicts with the Termux binding for naming a session


## Searching 

`g/` to search for a match to add when visual-multi is active, rather than the usual `/` vim search.

`n` and `N` can't be used to repeat the search, as they are used to get the next visual-multi match.


## Find with Regex 

`\ \ /` followed by a regex pattern will create a selection with that pattern. 

`n` and `N` finds the next occurrence of the regex pattern


## Smart case change

`gc` In extend-mode will use smartcase to change a selection

- at main cursor, text is always inserted as typed
- at other cursors, if region text was fully uppercased, replacement will be uppercased as well
- if the region text was capitalized, the replacement will be as well


## Filter regions

`\ \ f` filter out (remove) regions based on pattern or expression. 

`C-x` to cycle filtering method:

- pattern: remove regions that don't match the pattern
- !pattern:  remove regions that match the pattern
- expression: remove regions that don't match the expression (same as below)


## Transform regions with expression

`\ \ e` to transform a region with a vim expression, run on each region

Placeholders can be used in the expression 

- `%t~ region's text as a string (as-is)
- `%f~ region's text evaluated as a floating point number
- `%n~ region's text evaluated as an integer number
- `%i~ region's index
- `%N~ total number of regions

Examples:
- `%f * 0.5` divide text of all regions by 2
- `%t ." ". %i ." / ". %n`  append index / total to text of each region
- `%i%2 ? %t : toupper(%t)`  uppercase all odd regions (1,3,5...)
- `%i%3-2 ? %t : ''`  delete every third region



## VM Motions

visual-multi supports vim motions although they behave differently as their result is dependent on the mode:

- `cursor mode` will move cursors
- `extend mode` motions extend selections

Unless *multiline-mode* is enabled motions are restricted to the current line and cannot cross line boundaries

Some *object-motions* and *various-motions* require *multiline-mode* and aliased to avoid conflict with VM mappings:

| vim | VM~ | Description                          |
|-----|-----|--------------------------------------|
|  /  | g/  | to next match (for all regions)      |
|  (  | (   | [count] sentences backward           |
|  )  | )   | [count] sentences forward            |
|  {  | {   | [count] paragraphs backward          |
|  }  | }   | [count] paragraphs forward           |
|  [( | g(  | go to [count] previous unmatched '(' |
|  [{ | g{  | go to [count] previous unmatched '{' |
|  ]) | g)  | go to [count] next unmatched ')'     |
|  ]} | g}  | go to [count] next unmatched '}'     |


## vm-operators

Visual-Multi supports several operators by default:

- `y` / `d` / `c` to yank / delete / change
- `gu` / `gU` to change text case

Visual-Multi uses its own registers that are lists of strings. One element for each region that is yanked/deleted. 

There is also built-in support for:

- vim-surround  e.g. `ysiw(` to enclose in parentheses
- vim-abolish e.g. `cr_` to change current word to snake case

> `:help g:VM_user_operators to disccover how to doefine other operators 


## vm-multiline-mode

In normal and insert mode, cursors and selections are kept within their own line.  Cursors are blocked from moving off the current line to the next line.

`M` enables multiline-mode that allows cuursors to move onto another line.

Multiline mode must be enabled for an object motions, or they will fail. See |vm-motions|.


## Alignment 

`\\a` aligns by setting the minimum column to the highest of all regions
`\\<` aligns by character, or [count] characters
`\\>` aligns by regex pattern

In extend-mode selections are collapsed to cursors first, although will work regardless.


## Replace pattern in regions 

`R` to replace with a pattern and then the replacement text

substitution will take place in all selected regions, leaving unselected text untouched.

Only working in |extend-mode|. When |R| is pressed in |cursor-mode|, it will start |vm-replace-mode| instead.


## Subtract pattern from regions 

`\\s` subtract the entered pattern from regions, splitting them. Only working in |extend-mode|.


## Transposition

`\ \ t` swaps the contents of selections, cycling them if there are more than two.

If there is an equal number of selections in each line, swapping takes place within the same line only. Only in |extend-mode|.


## Duplication

`\ \ d` duplicates in place the contents of the selections, reselecting the original ones. Only in extend-mode.


## Shift Selections

<M-S-Right> and <M-S-Left> move the selections right or left, preserving the surroundings.


## Case conversion

`\\C` runs on inner words in cursor mode 

- `u` lowercase
- `U` UPPERCASE
- `C` Captialize
- `t` Title Case
- `c` camelCase
- `P` PascalCase
- `s` snake_case
- `S` SNAKE_UPPERCASE
- `-` dash-case
- `.` dot.case
- `<space>` space case


## Modes

*cursor-mode* and *extend-mode* are two Visual-Multi modes, roughly corresponding to *normal-mode* and *visual-mode*

`TAB` switches between cursor-mode and extended-mode


### VM Cursor Mode

cursor-mode commands expect a motion, e.g. `c` should be followed by a text object to be changed. 

| `operators | see vm-operators                                          |
| `motions   | see vm-motions                                            |
| `|`        | set column for all cursors (to current column or [count]) |
| `r`        | replace single character                                  | 
| `R`        | enter vm-replace-mode                                     | 
| `~`        | change case of single character                           | 
| `&`        | repeat last substitution                                  | 
| `<C-A>`    | increase numbers                                          | 
| `<C-X>`    | decrease numbers                                          | 
| `g<C-A>`   | progressively increase numbers (`v_g_CTRL-A`)             |
| `g<C-X>`   | progressively decrease numbers (`v_g_CTRL-X`)             |

You can enter |insert-mode| with `i`, `I`, `a`, `A`, and only from cursor mode also with `o` and `O`.

Also see `vm-motions` for supported motions in VM (some with differences).


### VM Extend Mode

extend-mode is like having multiple visual selections.  motions extend the slections and change / yank / delete commands don't wait for a motion, just like in visual mode. 

Even the key `o` works as in visual mode, inverting the anchor of the selections.

Some commands are specific to |extend-mode|, such as:

- `s` vim-surround
- `R` replace pattern in regions
- `\\s` split regions by pattern
- `\\e` transform regions text with vim expression

Some commands enforce *cursor-mode* when run from *extend-mode*:

- `<C-A>` increase numbers
- `<C-X>` decrease numbers

Others can use a different mapping:

- `gu/gU` change case (instead of vim `u` / `U`)
- `o` and `O` mappings are used to invert the facing of the selected regions and not to start insert mode.

