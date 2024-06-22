# Neovim Registers

Neovim use registers to store and access text using Neovim commands.

++double-quote++ to access a register by name.

The name of a register is a number, alphabetical or special character.

`SPC f r` lists the values of registers in a telescope popup

??? EXAMPLE "Yank and paste commit message"
    Select the text of the commit message

    ++double-quote++ ++"m"++ ++"y"++ yanks the selected text into register `m`

    Complete the Git commit.  When creating a new commit, paste the message from the register

    ++double-quote++ ++"m"++ ++"p"++ pastes the register text into the commit message buffer

??? EXAMPLE "Paste last evaluation result from Conjure"
    When Conjure evaluates code the result is stored in the `C` register.

    ++double-quote++ ++"C"++ ++"p"++ pastes the register text into the commit message buffer

## Registers

!!! INFO "Neovim help - registers"
    ```shell
    :help registers
    ```

++double-quote++ the unnamed register, used by Neovim normal commands, e.g. `c` `d` `p` `s` `x` `y`, etc.

++0++ to ++9++ numbered registers containing yank and delete history

++minus++ small delete register for text smaller than a line

++"a"++ to ++"z"++ named registers manually selected, ++"A"++ to ++"Z"++ to append to the text already in the register

++colon++ ++period++ and ++"%"++ read-only registers use with put commands (last inserted, current file name, recent command)

++"#"++ alternate buffer file name

++equal++ expression register for the result of runing a Neovim command expression

++plus++ and ++"*"++ selection registers for GUI

++underscore++ black hole register does not store text, use when normal commands shouldnt update other registers

++slash++ last search pattern register used


## Find Registers

`SPC f r` opens the list of registers in a telescope popup.

![AstroNvim Find Registers - telescope view](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-find-registers-telescope-popup-light.png?raw=true#only-light){loading=lazy}
![AstroNvim Find Registers - telescope view](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-find-registers-telescope-popup-dark.png?raw=true#only-dark){loading=lazy}


!!! HINT "Registers in insert mode"
    `C-r` in insert mode pastes the content of the given register, e.g. `C-r a` to paste the content of `"a`
