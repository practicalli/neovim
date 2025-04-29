# Spectre

++spc++ ++"s"++ ++"s"++ to toggle Spectre (open/close) to search and replace tool.

`?` for the Spectre key mappings

![Neovim Spectre key mappings](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-search-replace-spectre-mappings-dark.png?raw=true#only-dark){loading=lazy}


## Search & Replace

++"i"++ underneath Search and enter a search pattern, ++esc++ to see resuts in a popup below.

++"i"++ underneath Replace and enter a replace pattern, ++esc++ to see in-line diff results

> ++"v"++ toggles Spectre results view between diff to search to replace view

![Neovim Spectre search replace](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-search-replace-spectre-search-dark.png?raw=true#only-dark){loading=lazy}
![Neovim Spectre search replace](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-search-replace-spectre-search-dark.png?raw=true#only-light){loading=lazy}


++"d"++ ++"d"++ to toggle an occurance 

 ++"R"++ replaces all occurances (after selecting the occurances to change)

A DONE checkbox is show at then end of each selection which has been reaplaced

> To replace single occurance, toggle all occurances that should not be changes and press ++"R"++

![Neovim Spectre search replace done](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-search-replace-spectre-search-partial-replaced-dark.png?raw=true#only-dark){loading=lazy}
![Neovim Spectre search replace done](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-search-replace-spectre-search-partial-replaced-dark.png?raw=true#only-light){loading=lazy}


!!! HINT "Spectre does not undo changes"
    Use Git or Neovim undo to rollback changes made by Spectre.


[:globe_with_meridians: Spectre](https://github.com/nvim-pack/nvim-spectre){target=_blank} is available via the AstroNvim Community project pack and included in the Practicalli astronvim-config    

[:globe_with_meridians: ripgrep](https://github.com/BurntSushi/ripgrep){target=_blank} and [:globe_with_meridians: sed](https://www.gnu.org/software/sed/) are required.

[:fontawesome-brands-github: Spectre project](https://github.com/nvim-pack/nvim-spectre){target=_blank .md-button}    

