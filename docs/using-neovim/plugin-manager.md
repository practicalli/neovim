# Lazy Plugin manager & Mason tool manager

Neovim community provides a wide range of plugins to extend the features of Neovim.

There is a basic built-in plugin manager although the Neovim roadmap describes its intent as to support community plugin managers.

Lazy plugin manager creates a resource efficient use of Neovim by only loading plugins when needed and provides an excellent user experience.

Mason manages Language Server Protocol (LSP) servers, Debug Adaptor

!!! NOTE "Update everything"

    ++spc++ ++"p"++ ++"a"++ to update lazy plugins and mason tools


!!! TIP "Update again for AstroNvim plugins"
    A notification ... change in AstroNvim plugins.

    TODO: insert screenshot of notification

    `U` in the lay plugin runs the update again and installs the new plugins.


![AstroNvim Lazy plugin manager status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lazy-installed-after-config-update.png?raw=true#only-light){loading=lazy}
![AstroNvim Lazy plugin manager status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-lazy-installed-after-config-update.png?raw=true#only-dark){loading=lazy}


### Plugin status

The Lazy popup shows the plugins installed and there status and changelog.

The changelog is shown for updated plugins, highlighting breaking changes.  Conventional commits style is used for most plugins, making it easier to follow the most important changes.

`RET` on a plugin name expands to show the source of the plugin.


TODO: example plugin changelog
