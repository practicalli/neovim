# Evil G menu

g` in normal mode opens a menu of convenient utilities.  Practicalli uses this menu to comment existing lines, jumping to top or bottom of the buffer and changing text case.


## Comment lines and regions

`g c c` will comment the current line using the buffer major mode comment character(s).  A prompt will ask if no comment character is set for the major mode.

`g c` with a selected region will comment all lines with the major mode comment character(s)


## Jumping around

`g g` jumps to the top of the buffer, `g G` to the bottom of the buffer

`g d` to jump to the source code of a function definition, `g D` to open that in a different window.

`g f` to jump to file name under cursor (if file exists).


## Changing text case

`g u` to change the current character or selection to lowercase, `g U` for uppercase.

> #### Hint::Toggle case with `~`
> `~` will toggle the case of the current character or selected region.

<!--
## Marks

> TODO: using marks with g menu
--->
