# Using Neovim

The fundamental controls of Neovim which apply across all editing tasks.

## Fundamentals

[:fontawesome-solid-book-open: Multi-modal Editing](multi-modal-editing.md){.md-button}
[:fontawesome-solid-book-open: File Buffer Window and Tab page](file-buffer-window-tab.md){.md-button}




## Editing Tools

[:fontawesome-solid-book-open: Multiple Cursors](multiple-cursors.md){.md-button}


## Writing Tools

[:fontawesome-solid-book-open: Snippets](snippets.md){.md-button}


## Development Tools

[:fontawesome-solid-book-open: Comments](comments.md){.md-button}
[:fontawesome-solid-book-open: Clojure Development](../repl-driven-development/index.md){.md-button}
[:fontawesome-solid-book-open: Version Control](../version-control/index.md){.md-button}

> Format and Lint tools are installed via Mason

<!-- ![Neovim startup with dashboard theme](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-startup-dashboard-theme-light.png) -->



## Keyboard mappings

`:verbose map` followed by a key binding shows the location of the configuration that was last used to set the key mapping.  Use when its not clear what command a key mapping is calling or if a plugin is over-riding an expected mapping. 

++spc++ ++"f"++ ++"n"++ to list all notifications and ++enter++ on the relevant notification to see the details.


`:verbose map <C-Up>` shows the last place in the neovim config that defines a mapping for ++ctrl+arrow-up++.

[Map Listing: Neovim docs](https://neovim.io/doc/user/map.html#map-listing){target=_blank .md-button}
[Key Notation: Neovim docs](https://neovim.io/doc/user/intro.html#key-notation){target=_blank .md-button}

