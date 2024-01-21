# Neovim Registers

Neovim use registers to store and access text using Neovim commands.

++double-quote++ to access a register by name.

The name of a register is a number, alphabetical or special character.

`SPC f r` lists the values of registers in a telescope popup


!!! EXAMPLE "Yank and paste commit message"
    Select the text of the commit message

    ++double-quote++ ++"m"++ ++"y"++ yanks the selected text into register `m`

    Complete the Git commit.  When creating a new commit, paste the message from the register

    ++double-quote++ ++"m"++ ++"p"++ pastes the register text into the commit message buffer

## Special Registers



## Find Registers

`SPC f r` opens the list of registers in a telescope popup.

![AstroNvim Find Registers - telescope view](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-find-registers-telescope-popup-light.png?raw=true#only-light){loading=lazy}
![AstroNvim Find Registers - telescope view](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-find-registers-telescope-popup-dark.png?raw=true#only-dark){loading=lazy}
