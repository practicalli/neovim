# Plugin Manager

Neovim community provides a wide range of plugins to greatly extend the features of Neovim

There is a wide range of plugin managers too, including a built-in plugin manager in Neovim.

* Lazy - AstroNvim Config
* Packer - Practicalli Neovim Config Redux

!!! HINT "Lazy plugin manager recommeded"
    Practicalli recommends Lazy plugin manager as it feels much easier to use and has a more engaing and understandable user interface

??? WARNING "Neovim evolving"
    Neovim and its plugins are evolving quite rapidly, so it is recommended to update plugins if there are issue or when a newer version of Neovim has been installed

    Plugin issue are not that common and typically fixed quite quickly by the community

=== "AstroNvim"
    Lazy plugin manager

    ![AstroNvim Lazy plugin manager status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lazy-installed-after-config-update.png?raw=true#only-light){loading=lazy}
    ![AstroNvim Lazy plugin manager status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lazy-installed-after-config-update.png?raw=true#only-dark){loading=lazy}

=== "Practicalli Neovim Config Redux"

    `SPC P u` to update packages to their latest versions (`:PackerUpdate`).  Details of updated changes will be shown at the end of the update.
    
    ![Neovim Packer - packages updated report](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-packer-sync-updated-packages.png)
    
    `r` in the package update screen gives the option to revert an update if something has gone wrong (although this seem to be a rare issue).
    
    When packages are all at the latest available version, Packer update reports packages already up to date.
    
    ![Neovim Packer update everything up to date](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-packer-update-already-up-to-date.png)
    
    > Packer downloads packages and documentation from the Internet, so a connection is required


## Package List and documentation

=== "AstroNvim"
    Lazy plugin manager


=== "Practicalli Neovim Config Redux"

    `SPC P l` to list the current packages added to the configuration
     
    ![Neovim Package list with telescope](https://raw.githubusercontent.com/practicalli/graphic-design/live/editors/neovim/screenshots/neovim-packer-telescope-package-list.png)
    
    Selecting a package will display the website documentation for the package (although this may be in HTML so not the cleanest way to read the docs).


## Adding packages

=== "AstroNvim"
    Lazy plugin manager

=== "Practicalli Neovim Config Redux"
    Add package names as keywords in the `use` expression in `fnl/config/plugin.fnl` file.

    `:requires` to add a package that is a dependency for the package being added
    
    `:mod` defines the namespace that contains the package configuration, typically a `setup` function with options.  The namespace matches the file name under `fnl/config/plugin`

    `SPC P i` to install packages that have been added to `fnl/config/plugin.fnl`

    `q` to quit once all packages are up to date
