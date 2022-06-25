# Nvim Treesitter

Treesitter provides language specific parsing, highlight and indent features and so is a fundamental plugin to use with Neovim.

`clojure`, `fennel` and `markdown` parsers are automatically installed in the practicalli/neovim-config-redux configuration.

* `:TSInstallInfo` lists language parsers and install status 
* `:TSUpdate {language}` to update a parser to the latest compatible version (specified in nvim-treesitter lockfile.json).
* `:TSInstall {language}` compiles and installs a parser for the given language.

## nvim-treesitter configuration

`clojure`, `fennel` and `markdown` parsers are automatically installed in the practicalli/neovim-config-redux configuration.

highlight and indent modules are enabled by default

In `fnl/config/plugin/treesitter.fnl`

```fennel
(module config.plugin.treesitter
  {autoload {treesitter nvim-treesitter.configs}})

(treesitter.setup {:highlight {:enable true}
                   :indent {:enable true}
                   :ensure_installed ["clojure" "fennel" "markdown"]})
```

## Manually Install Parsers

nvim-treesitter provides the `TSInstall` command to generate a parser for a specific language, assuming that language is supported.

> A compiler (gcc, clang, etc) should be installed in the operating system on which nvim is running

```
:TSInstall {language}
```
> `TAB` completion lists the available language parsers, `TAB` and `S-TAB` to navigate the auto-completion popup.


## Automatically update parsers

When nvim-treesitter is updated, it is recommended that the parsers are Automatically updated too.

> TODO: configure practicalli/neovim-config-redux to automatically update parsers

