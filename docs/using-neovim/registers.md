# Neovim Registers

Neovim use registers to store and access text using Neovim commands.

++double-quote++ to access a register by name.

The name of a register is a number, alphabetical or special character.

++spc++ ++"f"++ ++"r"++ [lists the values in all registers](#find-registers) in a picker popup.

??? EXAMPLE "Yank and paste commit message"
    Select the text of the commit message

    ++double-quote++ ++"m"++ ++"y"++ yanks the selected text into register `m`

    When creating a new commit, paste the message from the register

    ++double-quote++ ++"m"++ ++"p"++ pastes the register text into the commit message buffer

??? EXAMPLE "Paste last evaluation result from Conjure"
    When Conjure evaluates code the result is stored in the `c` register.

    ++double-quote++ ++"c"++ ++"p"++ pastes the register text into the commit message buffer


## Register menu

++double-quote++ popup shows the current registers in use and a summary of there contents.

![Neovim registers popup menu](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-registers-popup-dark.png?raw=true#gh-dark-mode-only){loading=lazy}
![Neovim registers popup menu](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-registers-popup-light.png?raw=true#gh-light-mode-only){loading=lazy}


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

++equal++ expression register for the result of running a Neovim command expression

++plus++ and ++"*"++ selection registers for GUI

++underscore++ black hole register does not store text, use when normal commands shouldn't update other registers

++slash++ last search pattern register used


## Find Registers

++spc++ ++"f"++ ++"r"++  opens the list of registers in a telescope popup.

![AstroNvim Find Registers - telescope view](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-find-registers-popup-dark.png?raw=true#only-dark){loading=lazy}
![AstroNvim Find Registers - telescope view](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-find-registers-popup-light.png?raw=true#only-light){loading=lazy}


!!! HINT "Registers in insert mode"
    ++ctrl+"r"++ in insert mode pastes the content of the given register, e.g. ++ctrl+"r"++ ++"a"++ to paste the content of `"a`
