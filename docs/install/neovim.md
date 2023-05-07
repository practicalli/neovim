# Install Neovim

[Neovim releases](https://github.com/neovim/neovim/releases){target=_blank .md-button}

Neovim 8 is the minimum version for this configuration and Neovim 0.9.0 is currently being tested.  

Follow the [install Neovim guide for the specific operating system](https://github.com/neovim/neovim/wiki/Installing-Neovim){target=_blank}.

Neovim 9 only provides an AppImage install for Linux.  For an nvim binary, extract the AppImage or build Neovim from source, optionally creating a Debian/Ubuntu package.


??? EXAMPLE "Extract AppImage"
    ```shell
    chmod a+x ./nvim.appimage
    ./nvim.appimage --appimage-extract
    ```

??? EXAMPLE "Extract AppImage via GitHub Workflow"
    ```yaml
      - name: Install Neovim
        shell: bash
        run: |
          mkdir -p /tmp/nvim
          wget -q https://github.com/neovim/neovim/releases/download/nightly/nvim.appimage -O /tmp/nvim/nvim.appimage
          cd /tmp/nvim
          chmod a+x ./nvim.appimage
          ./nvim.appimage --appimage-extract
          echo "/tmp/nvim/squashfs-root/usr/bin/" >> $GITHUB_PATH
    ```

## Suppoting Tools 

=== "Debian / Ubuntu"
    Install the following packages to support Neovim

    - `ripgrep` fast file contents search (used by telescope)
    - `find-fd` advanced search tool 
    - `xclip` clipboard 

    ```shell
    sudo apt install find-fd xclip
    ```

   `set clipboard+=unnamedplus` in the Neovim configuration instructs Linux to use the clipboard tool 

    ??? INFO "Wayland requires wl-clipboard"
    Install the `wl-clipboard` package to use the Wayland desktop clipboard with Neovim
    ```shell
    sudo apt install wl-clipboard
    ```
    
## Build Neovim from Source

Clone the [Neovim GitHub repository](https://github.com/neovim/neovim/wiki/Building-Neovim) 

```shell
git clone 
```

Change into the cloned directory and change to the `stable` release to build version 0.9.0

```shell
git checkout stable
```

Build a release

```shell
make CMAKE_BUILD_TYPE=Release                                                                                                              ─╯
```

### Build dep package 

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
