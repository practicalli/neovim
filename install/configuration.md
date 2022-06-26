# Neovim Configuration

[practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) provides a complete Fennel based configuraion for Neovim, with a wide range of plugins and associated setup and key bindings.

Clone [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) to `~/.config` directory (or a preferred location and create a symbolic link).

```bash
git clone https://github.com/practicalli/neovim-config-redux.git
```

> Create a fork of [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) first if intending to customise this configuration


## `init.lua`
 - bootstraps the [aniseed package](https://github.com/Olical/aniseed) which compiles the Fennel configuration into Lua, which is then read by Neovim. Defines the entry point to the Fennel configuration as `fnl/config/init.fnl`
 - installs ([packer.nvim](https://github.com/wbthomason/packer.nvim)) for package management


## `fnl/config/init.fnl`

- load plugin configuration namespace `config.plugin`
- load `config.util` namespace to streamline key binding definitions
- set the leader key as `space` and local-leader as `,`
- define key bindings - uses config.util  (mapping to be moved to their own namespace)
- set global Neovim options


## `fnl/config/plugin.fnl`

Define plugins to add functionality to Neovim.

`use` is a private function that searches the plugin configuration map for the keyword `:mod` and loads the associated namespace (namespace defined with a keyword with the same name)

e.g. in the telescope plugin configuration `:mod` has a value of `:telescope` which will load the file `fnl/config/plugin/telescope.fnl`

```clojure
  :nvim-telescope/telescope.nvim
  {:requires [:nvim-lua/popup.nvim
              :nvim-lua/plenary.nvim]
   :mod :telescope}
```

Packer downloads the `nvim-telescope/telescope.nvim` plugin and all the plugins in `:requires` section and search for the namespace `telescope`
in file located in the following path `fnl/config/plugin/telescope`


## `fnl/config/plugin/conjure.fnl`

Conjure specifics settings

> TODO: review the Conjure configuration options

<!-- Rafael config: , remap doc keymap `K` to `<localleader>K`, avoiding conflict with the LSP docs `K` -->


## `fnl/config/plugin/telescope.fnl`

Settings like ignore `node_modules` and everything in `.gitignore` to be listed in the file finder.

Defines a ripgrep command to set parameters for searching files

Add `--hidden` to see all dotfiles (regardless of .gitignore patterns)

<!-- TODO: review ripgrep arguments - find args that respect .gitignore and show dotfiles too -->

Keymaps:
 - `<leader>ff` open the find files
 - `<leader>fg` open the fuzzy finder
 - `<leader>fb` open the find open buffer
 - `<leader>fh` open the nvim help fuzzy finder


## `fnl/config/plugin/treesitter.fnl`

Defines which language parsers and modules to use.

- automatically use `clojure`, `fennel` and `markdown` parsers (and compile on first run of Neovim)
- automatically update language parsers when nvim-treesitter plugin updated
- enable highlight module
- enable indent module

```clojure
(treesitter.setup
  {:ensure_installed ["clojure" "fennel" "markdown"]
   :sync_install true
   :highlight {:enable true}
   :indent    {:enable true}})
```


## `fnl/config/plugin/lspconfig.fnl`

Language Server Protocol for static analysis of code, to provide common formatting, linting and refactoring tooling across all programming languages.

Define which symbols to show for lsp diagnostics

```clojure
(defn define-signs
  [prefix]
  (let [error (.. prefix "SignError")
        warn  (.. prefix "SignWarn")
        info  (.. prefix "SignInfo")
        hint  (.. prefix "SignHint")]
  (vim.fn.sign_define error {:text "" :texthl error})
  (vim.fn.sign_define warn  {:text "" :texthl warn})
  (vim.fn.sign_define info  {:text "" :texthl info})
  (vim.fn.sign_define hint  {:text "" :texthl hint})))
```

- features and server settings to enable/customize.
  - Handler defines features and how we want to render the server outputs.
  - Capabilities we link with our autocompletion plugin (nvim-cmp), to say to the lsp servers that we have this feature enabled.
  - On_Attach we customize our interaction with the LSP server, here we define the following keymaps:
- configure all settings above in clojure-lsp server instance.


### `fnl/config/plugin/cmp.fnl`

Configure sources to show in the autocomple menu (i.e. conjure, lsp, buffer) and key bindings to navigate the autocomplete popup menu.


## `fnl/config/plugin/theme.fnl`

Add the [Neovim GitHub theme](https://github.com/projekt0n/github-nvim-theme) which gives 3 dark and 3 light themes to choose from.  Individual colors and styles can be configured to change specific parts of the theme.

The light theme is used by default, with a custom softer background colour that is slightly red-shifted.

Options are specified in the `theme.setup` function, where the option names are keywords and the values are strings, boolean or hash-map of more option keywords and values.

```
(theme.setup {:theme_style "light"
              :colors {:bg "#f8f2e6"}
              :comment_style "italic"})
```

The colors (Hex values) for each theme are in the [github-nvim-theme/lua/github-theme/palette](https://github.com/projekt0n/github-nvim-theme/tree/main/lua/github-theme/palette) with the overal theme definition in [github-nvim-theme/lua/github-theme/theme.lua](https://github.com/projekt0n/github-nvim-theme/blob/main/lua/github-theme/theme.lua)


## `fnl/config/plugin/sexp.fnl`

Settings for vim-sexp like enabling it for another lisp languages like Fennel and Jannet


### `fnl/config/plugin/lualine.fnl`

Configure the status line (lualine) that shows at the bottom of Neovim, defining colors and elements that appear on that line.

The Neovim GitHub theme includes definitions to set the look of the status line.
