# Narrowing

Narrowing to a region enables vim commands to be applied to a specific part of the current buffer, rather than the whole buffer.

Common examples include
- replacing local variables within a specific function (avoiding affecting other function definitions)

## NrrwRgn plugin

[:fontawesome-brands-github: NrrwRgn plugin](https://github.com/chrisbra/NrrwRgn) is inspired by the [:globe_with_meridians: Narrowing feature of Emacs](http://www.emacswiki.org/emacs/Narrowing)
and means to focus on a selected region while making the rest inaccessible.


![NrrwRgn plugin](https://github.com/chrisbra/NrrwRgn/raw/master/screencast.gif){loading=lazy}


## Yode plugin

[yode-nvim](https://github.com/hoschi/yode-nvim){target=_blank} will focus on selected text within a file.

Narrow by replacing the current buffer

- `YodeCreateSeditorReplace` focus on a code part and replace it with the current buffer
- `YodeBufferDelete` delete the current buffer and jump back to file, if it is a seditor

Or narrow using a floating window

- YodeCreateSeditorFloating focus on a code part and make it floating, stay at the current (main) view


[hoschi/yode-nvim](https://github.com/hoschi/yode-nvim){target=_blank .md-button}

<!--

Previously configured mappings for NrrwRgn plug

`SPC n r` opens a select region in a new split window.  The original buffer is protected from changes.

`:w` to write changes in the narrowed window to the original buffer


## Commands

- `:NR`   Open the selected region in a new narrowed window
- `:NW`   Open the current visual window in a new narrowed window
- `:WR`   (In the narrowed window) write the changes back to the original buffer.
- `:NRV`  Open the narrowed window for the region that was last visually selected.
- `:NUD`  (In a unified diff) open the selected diff in 2 Narrowed windows
- `:NRP`  Mark a region for a Multi narrowed window
- `:NRM`  Create a new Multi narrowed window (after :NRP) - experimental!
- `:NRS`  Enable Syncing the buffer content back (default on)
- `:NRN`  Disable Syncing the buffer content back
- `:NRL`  Reselect the last selected region and open it again in a narrowed window

Appending `!` to most commands opens the narrowed part in the current window instead of a new window.

> `:WR!` closes the narrowed window in addition to writing to the original buffer.


## Documentation

`:help NarrowRegion` to view the documetation on the NrrwRgn plug use


### Attention

`:NRM` is described as experimental by the project readme.

-->
