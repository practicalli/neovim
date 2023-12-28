# Install Neovim

 The [:fontawesome-brands-github: Neovim release page](https://github.com/neovim/neovim/releases){target=_blank} includes install steps for specific operating system.

Neovim 0.9 is the minimum version for this configuration and Neovim 0.9.4 is currently being used by Practicalli.

Follow the [install Neovim guide for the specific operating system](https://github.com/neovim/neovim/wiki/Installing-Neovim){target=_blank}.

[:fontawesome-brands-github: Neovim releases](https://github.com/neovim/neovim/releases){target=_blank .md-button}


## Suppoting Tools

Neovim uses several external tools for searching for files, search file contents and using the operating system clipbaord.

Install the following tools to support Neovim and AstroNvim

- `ripgrep` fast file contents search (used by telescope)
- `find-fd` advanced search tool
- `xclip` x11 clipboard as a provider for Neovim copy/paste (Linux only)
- `luarocks` for LSP servers (AstroNvim)

!!! INFO "Treesitter requires a C compiler"
    nvim-treesitter requires a C compiler , e.g. `gcc` for Linux or `clang` for android/termix

    The C compiler is used to compile langauge support for treesiter.


!!! INFO "AstroNvim requires node.js"
    AstroNvim uses Mason to install LSP servers, format and lint tools. Many of the LSP servers require node.

    [Node.js install - Practicalli Engineering Playbook](https://practical.li/engineering-playbook/programming-languages/javascript/nodejs/){target=_blank} 


=== "Debian Packages"

    !!! NOTE ""
        ```shell
        sudo apt install fd-find xclip luarocks
        ```

    Add `set clipboard+=unnamedplus` to the Neovim configuration to use the Linux clipboard tool

    ??? INFO "Wayland requires wl-clipboard"
        Install the `wl-clipboard` package to use the Wayland desktop clipboard with Neovim
        !!! NOTE ""
            ```shell
            sudo apt install wl-clipboard
            ```

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

=== "MacOSX Homebrew"

    MacOSX requires the libintl and gettext tools as well as the other supporting tools.

    !!! NOTE ""
        ```shell
        brew install libintl gettext ripgrep fd luarocks
        ```

## Install Neovim

=== "Linux AppImage"

    Download the [Linux AppImage](https://github.com/neovim/neovim/releases/){target=_blank} from the Neovim Release page and place the file on the executable path, e.g. `$HOME/.local/bin`

    Make the AppImage executable

    ```shell
    chmod u+x $HOME/.local/bin/nvim.appimage
    ```

    Create a symbolic link called `nvim` to the nvim.appimage file.

    ```shell
    ln -s $HOME/.local/bin/nvim.appimage $HOME/.local/bin/nvim
    ```

    `nvim` command can now be run in a terminal from any directory.


=== "MacOSX Homebrew"
    
    Install from Homebrew or via the Neovim Release page

    **Homebrew**
    ```shell
    brew install neovim
    ```

    **Neovim Release**

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

## Post Install checks

Ensure supporting tools and binaries are available in the operating system by running the Neovim Heath Check.

`nvim` in a terminal to run NeoVim and check the installation is working without error.

![NeoVim - default startup message](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-startup-default-message.png){target=_blank}

`:checkhealth` to run a check supporting tools are available to NeoVim.

A report is generated and shown in NeoVim

`j` / `k` to scroll through the checkhealth report

Review the warnings and install tooling that is required for languages that will be used.

![NeoVim checkhealth report](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-checkhealth-report.png)

!!! HINT "Ignore Provider Warnings"
    It is safe to ignore language provider warnings.

    [Language Providers can be disabled](/neovim/reference/neovim/language-providers/) in the Neovim configuration to remove the warnings from `:checkhealth` report.  Examples of disabling language provders are in the [practicalli/neovim-config-redux configuration](https://github.com/practicalli/neovim-config-redux){target=_blank}, covered in the [Neovim Config](configuration/) install step
