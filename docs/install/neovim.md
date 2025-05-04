# Install Neovim and Supporting Tools

![Neovim Logo](https://raw.githubusercontent.com/practicalli/graphic-design/be612ddb29f6b9eef1641e91de6c747b70d7fef8/logos/neovim-logos/neovim-mark.svg){align=right loading=lazy style="height:150px;width:150px"}

!!! INFO "Neovim 0.11.x required"


## Suppoting Tools

Neovim uses several command line tools for searching for files and their contents, using the operating system clipbaord and compiling Treesitter language parsers.

- `ripgrep` fast file contents search (used by telescope)
- `find-fd` advanced search tool
- `xclip` for X11 clipboard integration or `wl-clipboard` for Wayland
- `node.js` and luarocks` for LSP servers
- a C compiler for treesitter language parsers, e.g. `gcc` or `clang`


??? INFO "node.js install guide"
    AstroNvim uses Mason to install LSP servers, format and lint tools. Many of the LSP servers require node.

    [Node.js install - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/programming-languages/javascript/nodejs/){target=_blank}


=== "Debian Packages"

    !!! NOTE "Install for X11 based desktop"
        ```shell
        apt install fd-find luarocks nodejs xclip
        ```

    !!! NOTE "Install for Wayland based desktop"
        ```shell
        apt install fd-find luarocks nodejs wl-clipboard
        ```

=== "MacOSX Homebrew"

    MacOSX requires the libintl and gettext tools as well as the other supporting tools.

    !!! NOTE ""
        ```shell
        brew install libintl gettext ripgrep fd luarocks
        ```

## Install Neovim

Install from [:fontawesome-brands-github: Neovim GitHub releases](https://github.com/neovim/neovim/releases/) for the latest version, use a Package manager if version 0.11 is available, or build from source.


=== "Linux AppImage"

    Download the [Linux AppImage](https://github.com/neovim/neovim/releases/){target=_blank} from the Neovim Release page and place the file on the executable path, e.g. `$HOME/.local/bin` or `/usr/local/bin/` for system wide use (e.g. root account).

    Make the AppImage executable

    ```shell
    chmod u+x $HOME/.local/bin/nvim.appimage
    ```

    Create a symbolic link called `nvim` to the nvim.appimage file (or rename the file to `nvim`)

    ```shell
    ln -s $HOME/.local/bin/nvim.appimage $HOME/.local/bin/nvim
    ```

    `nvim` command can now be run in a terminal from any directory.


=== "MacOSX Homebrew"

    Install from Homebrew or via the Neovim Release page

    ```shell
    brew install neovim
    ```

=== "MacOS Neovim Release"

    Download `nvim-macos.tar.gz` From the [**Neovim GitHub release page**](https://github.com/neovim/neovim/releases)

    Avoid "unknown developer" warning from MacOSX

    ```shell
    xattr -c ./nvim-macos.tar.gz
    ```

    Make a local apps directory for neovim (and other things like node.js, etc.)

    ```bash
    mkdir -P ~/.local/apps
    ```

    Extract the neovim archive

    ```bash
    tar zvxf nvim-macos.tar.gz -C ~/.local/apps/
    ```

    Create the `~/.local/bin/nvim` symbolic link to include Neovim on the OS execution path

    > `echo $PATH` to check `.local/bin` is included in the execution the path by the Operating System command line shell

    ```bash
    ln -s ~/.local/apps/nvim-macos/bin/nvim ~/.local/bin/nvim
    ```

    Run `nvim`  (or setup a Neovim configuration first, e.g. AstroNvim)


=== "MacOSX GitHub Release"

    From the [**Neovim GitHub release page**](https://github.com/neovim/neovim/releases):

    1. Install `libintl`and `gettext` (e.g. via `brew install libintl gettext`)
    2. Download **nvim-macos.tar.gz**
    3. Run `xattr -c ./nvim-macos.tar.gz` (to avoid "unknown developer" warning)
    4. Make local apps directory for neovim (and other things like node.js, etc.)

    ```shell
    mkdir -P ~/.local/apps
    ```

    5. Extract the neovim download

    ```shell
    tar zvxf nvim-macos.tar.gz -C ~/.local/apps/
    ```

    6. Create nvim symbolic link in `~/.local/bin` to include Neovim on the OS execution path (check `.local/bin` is added to the execution the path by the Operating System command line shell)

    ```shell
    ln -s ~/.local/apps/nvim-macos/bin/nvim ~/.local/bin/nvim
    ```

=== "Debian Package"

    !!! INFO "Linux version only packaged as AppImage from Neovim 0.9 onward"

    A `.deb` file can be created after [building Neovim from source](https://github.com/neovim/neovim/blob/master/BUILD.md).


=== "Build from Source"

    [:fontawesome-brands-github: Neovim build guide](https://github.com/neovim/neovim/blob/master/BUILD.md){target=_blank .md-button}

    [:fontawesome-brands-github: Neovim Build Prerequisites for each operating system](https://github.com/neovim/neovim/wiki/Building-Neovim#build-prerequisites)

    ??? INFO "Debian Packages"
        Install packages to support building Neovim
        ```shell
        sudo apt-get install ninja-build gettext cmake unzip curl
        ```

    Clone the [:fontawesome-brands-github: Neovim GitHub repository](https://github.com/neovim/neovim){target=_blank}

    ```shell
    git clone --origin neovim https://github.com/neovim/neovim.git
    ```

    Change into the cloned directory and change to the `stable` release to build version 0.9.0

    ```shell
    git checkout stable
    ```

    Build a release

    ```shell
    make CMAKE_BUILD_TYPE=Release
    ```

    Once the nvim release has been built, create a debian package for use with Ubuntu and Debian systems

    ```shell
    cpack -G DEB
    ```


## Add a configuration

Neovim is a powerful editor although a configuration adds valuable features for software engineering tasks.

[Practicalli Astro 5 configuration](astro5-configuration.md){.md-button}
