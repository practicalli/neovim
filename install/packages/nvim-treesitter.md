# Nvim Treesitter

Treesitter provides language specific parsing, highlight and indent features and so is a fundamental plugin to use with Neovim.

`clojure`, `fennel`, `markdown` and `org` parsers are automatically installed in the practicalli/neovim-config-redux configuration.

* `:TSInstallInfo` lists language parsers and install status
* `:TSUpdate {language}` to update a parser to the latest compatible version (specified in nvim-treesitter lockfile.json).
* `:TSInstall {language}` compiles and installs a parser for the given language.
* `:TSUpdateSync` to update all parsers to the latest available versions


## nvim-treesitter configuration

`clojure`, `fennel`, `markdown` and `org` parsers are automatically installed if not already available.

`:sync_install true` automatically updates the parsers when the nvim-treesitter plugin is updated.  Treesitter and its parsers are actively developed, so its important to ensure parsers are kept up to date.  This is the equivalent of manually running `:TSUpdateSync`.

Parser highlight and indent modules are enabled by default

In `fnl/config/plugin/treesitter.fnl`

```fennel
(module config.plugin.treesitter
  {autoload {treesitter nvim-treesitter.configs}})

(treesitter.setup
  {:ensure_installed ["clojure" "fennel" "markdown" "org"]
   :sync_install true
   :highlight {:enable true}
   :indent    {:enable true}})
```


## Manually Install Parsers

nvim-treesitter provides the `TSInstall` command to generate a parser for a specific language, assuming that language is supported.

> A compiler (gcc, clang, etc) should be installed in the operating system on which nvim is running

```
:TSInstall {language}
```
> `TAB` completion lists the available language parsers, `TAB` and `S-TAB` to navigate the auto-completion popup.
