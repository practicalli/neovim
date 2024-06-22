# Lazy Plugin Manager

Neovim community provides a wide range of plugins to greatly extend the features of Neovim

There is a wide range of plugin managers too, including a built-in plugin manager in Neovim.


??? HINT "Lazy plugin manager recommended"
    Practicalli uses Lazy plugin manager as it feels much easier to use and has a more engaing and understandable user interface


## Plugin Updates

++spc++ ++"p"++ ++"S"++ shows the install and loaded status for all plugins defined in the Neovim configuration, e.g. `lua/community.lua` and `lua/plugins/*.lua` files

++spc++ ++"p"++ ++"S"++ checks for updated plugin versions and automatically installs them

![AstroNvim Lazy plugin manager status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lazy-installed-after-config-update.png?raw=true#only-light){loading=lazy}
![AstroNvim Lazy plugin manager status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lazy-installed-after-config-update.png?raw=true#only-dark){loading=lazy}

The changelog is shown for all updated plugins, highlighting breaking changes.  Conventional commits style is used for most plugins, making it easier to follow the most important changes.
