# Install Neovim

[Neovim releases](https://github.com/neovim/neovim/releases){target=_blank .md-button}

Neovim 8 is the minimum version for this configuration and Neovim 0.9.0 is currently being tested.

Follow the [install Neovim guide for the specific operating system](https://github.com/neovim/neovim/wiki/Installing-Neovim){target=_blank}.


## Suppoting Tools

=== "Debian / Ubuntu"
    Install the following packages to support Neovim

    - `ripgrep` fast file contents search (used by telescope)
    - `find-fd` advanced search tool
    - `xclip` clipboard as a provider tools for Neovim copy/paste
    - `luarocks` for LSP servers (AstroNvim)

    !!! NOTE ""
        ```shell
        sudo apt install find-fd xclip luarocks
        ```

    Add `set clipboard+=unnamedplus` to the Neovim configuration to use the Linux clipboard tool

    ??? INFO "Wayland requires wl-clipboard"
        Install the `wl-clipboard` package to use the Wayland desktop clipboard with Neovim
        ```shell
        sudo apt install wl-clipboard
        ```

## Install Neovim

=== "Linux AppImage"

    Download the AppImage from the Neovim Release page and place the file on the executable path, e.g. `$HOME/.local/bin`

    Make the AppImage executable

    ```shell
    chmod u+x nvim.appimage
    ```

    Run neovim from the AppImage

    ```shell
    nvim.appimage
    ```

    Create a symbolic link called `nvim` to the nvim.appimage

    ```shell
    ln -s $HOME/.local/bin/nvim.appimage $HOME/.local/bin/nvim
    ```

=== "Ubuntu/Debian"
    Download the Linux AppImage from the Neovim Releases page

    Or build Neovim from source and generate a `.deb` file from the build.

    ??? INFO "Linux version only packaged as AppImage from Neovim 0.9 onward"

=== "Build from Source"

    [Neovim Build Prerequisites for each operating system](https://github.com/neovim/neovim/wiki/Building-Neovim#build-prerequisites)

    ??? INFO "Ubuntu/Debian Packages"
        Install packages to support building Neovim
        ```shell
        sudo apt-get install ninja-build gettext cmake unzip curl
        ```

    Clone the [Neovim GitHub repository](https://github.com/neovim/neovim/wiki/Building-Neovim)

    ```shell
    git clone --origin neovim https://github.com/neovim/neovim.git
    ```
    Change into the cloned directory and change to the `stable` release to build version 0.9.0

    ```shell
    git checkout stable
    ```

    Build a release

    ```shell
    make CMAKE_BUILD_TYPE=Release                                                                                                              ─╯
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
