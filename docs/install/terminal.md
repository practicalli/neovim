# Terminal Tools and Fonts

Neovim is a terminal based application so use of a quality terminal is recommended, e.g. Kitty Terminal (or iTerm2 if only on MacOSX)

External Command line tools support search and other system information based features presented in AstroNvim.

Nodejs supports Language Server protocol servers, format and lint tools installed by Mason.


## Kitty Terminal with Nerd Fonts

Neovim runs in a terminal, so using Kitty (or iTerm2 - MacOSX only) are recommended.  Kitty provides Nerd fonts for additional symbols on top of the terminal font, providing a richer experience.

[:globe_with_meridians: Kitty Terminal - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/command-line/kitty-terminal/) provides examples of using Nerd Fonts or Nerd Font symbols with the Kitty terminal.

[Nerd Fonts](https://www.nerdfonts.com/)


## Command line tools

- ripgrep text search tool
- fzf fuzzy finder
- gdu
- btm from [:fontawesome-brands-github: GitHub repository releases](https://github.com/ClementTsang/bottom/releases/)

=== "Debian packages"
    Install fzf, gdu and node.js via debian package manager
    ```shell
    apt install fzf gdu
    ```

=== "Homebrew"
    Install fzf, gdu and node.js via Homebrew package manager
    ```shell
    brew install fzf gdu
    ```

Install btm from its [:fontawesome-brands-github: GitHub repository release page](https://github.com/ClementTsang/bottom/releases/)



## nodejs for LSP, format & lint tools

AstroNvim uses Mason to install LSP servers, format and lint tools.  Many LSP servers require node.js to install and function.

[Node.js install - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/programming-languages/javascript/nodejs/){target=_blank .md-button}
