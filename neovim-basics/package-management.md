# Manage packages with Packer

Some Neovim packages are quite new, especially those using treesitter.  It is recommended to update the packages if there are issue or when a newer version of Neovim has been released

`SPC P u` to update packages to latest versions (`:PackerUpdate`)

`r` in the package update screen gives the option to revert an update if something has gone wrong (although this seem to be a rare issue).

![Neovim Packer update everything up to date](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-packer-update-already-up-to-date.png)

> Packer downloads packages and documentation from the Internet, so a connection is required

## Package List and documentation

`SPC P l` to list the current packages added to the configuration

![Neovim Package list with telescope](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-packer-telescope-package-list.png)

Selecting a package will display the website documentation for the package (although this may be in HTML so not the cleanest way to read the docs).


## Adding packages

Add package names as keywords in the `use` expression in `fnl/config/plugin.fnl` file.

`:requires` to add a package that is a dependency for the package being added

`:mod` defines the namespace that contains the package configuration, typically a `setup` function with options.  The namespace matches the file name under `fnl/config/plugin`

`SPC P i` to install packages that have been added to `fnl/config/plugin.fnl`

`q` to quit once all packages are up to date
