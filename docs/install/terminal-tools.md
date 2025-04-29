# Terminal Tools and Fonts

Neovim is a terminal based application and [Kitty Terminal](#kitty-terminal) is highly recommended.

File system search and other system information based features presented in AstroNvim relies on [external command line tools](#command-line-tools).

Language Server Protocol servers, format and lint tools managed by Mason often require [Nodejs](#nodejs) to install & run.


## Kitty Terminal

Kitty Terminal provides multiple shell tabs, Nerd fonts, web icons and graphics support too, so is an excellent choice for running Neovim.  Kitty is available on all good operating systems.

[:fontawesome-solid-book-open: Kitty Terminal - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/os/command-line/kitty-terminal/){target=_blank .md-button}


## Command line tools

- [:fontawesome-brands-github: ripgrep](https://github.com/BurntSushi/ripgrep) fast text search tool
- [:fontawesome-brands-github: fzf](https://github.com/junegunn/fzf) fuzzy finder
- [:fontawesome-brands-github: gdu](https://github.com/dundee/gdu) disk usage analyzer
- [:fontawesome-brands-github: bottom (btm)](https://github.com/ClementTsang/bottom) graphical process/system monitor for the terminal


=== "Debian packages"
    Install fzf, gdu and node.js via debian package manager
    ```shell
    apt install ripgrep fzf gdu
    ```

=== "Homebrew"
    Install ripgrep, fzf, gdu and node.js via Homebrew package manager
    ```shell
    brew install ripgrep fzf gdu nodejs
    ```

Install btm from its [:fontawesome-brands-github: GitHub repository release page](https://github.com/ClementTsang/bottom/releases/){target=_blank}


## Nodejs

AstroNvim uses Mason to install LSP servers, format and lint tools.  Many LSP servers require node.js to install and function.

[Node.js install - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/programming-languages/javascript/nodejs/){target=_blank .md-button}
