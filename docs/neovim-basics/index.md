# Using Neovim

The fundamental controls of Neovim which apply across all editing tasks.

## Fundamentals

[:fontawesome-solid-book-open: Files, buffers and windows](files-buffers-windows.md){.md-button}
[:fontawesome-solid-book-open: Multi-modal Editing](multi-modal-editing.md){.md-button}

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


## Spellcheck

=== "AstroNvim"

    `SPC u s` toggles spellcheck, marking misspelt words with a rew wavy underline

    `] s` jumps to next misspelt word, `[ s` jumps to previous misspelt word, 

    `z =` shows numbered list of possible words, enter the number next to the work to replace the misspelt word.

    `z g` to add the current word to the spell list, infroming spellcheck that this is a correct word.
