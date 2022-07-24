# Add Neovim Packages

> #### Hint::WIP: Check the [practicalli/neovim-config-reduct configuration](https://github.com/practicalli/neovim-config-redux)
> Many packages have been added to the configuration and `fnl/config/package.fnl` is the most up to date list of packages currently used.

List of packages and their purpose

| Package               | Description                                                          |
|:----------------------|:---------------------------------------------------------------------|
| conjure               | Clojure REPL Driven Development (and other language REPLs)           |
| sexp                  | Structured Editing                                                   |
| newpaper theme        | Clean and simple UI & colour scheme, aimed at readably               |
| [lualine](lualine.md) | Fast and configurable statusline                                     |
| nvim-treesitter       | Parse code highly efficiently, client for LSP servers                |
| telescope             | Completion tool, e.g. select files, buffers tabs, packages, etc      |
| nvim-tree             | Visual file manager - open, create, delete, etc. files & directories |
| neogit                | Magit style visual Git client                                        |
| Octo                  | Git Issues and Pull Requests                                         |
| gitsigns              | Show diff changes in buffer gutter and status line                   |

Any specific package configuration & key bindings (on sub page if significant content)


## Package selection criteria

Packages are more likely to be adopted if:

- provide valuable (or fun) features
- work reliably, without generating errors
- do not conflict with other valuable packages in this configuration
- written in fennel or lua to aid maintenance
- use features provided by Neovim (e.g treesitter)
- are well documented
- are easy to configure
- are easy to use
- work well with themes (where relevant)


<!-- ## Plugins (from project readme.md) -->
<!--  - [packer](https://github.com/wbthomason/packer.nvim) *Plugin/package management* -->
<!--  - [aniseed](https://github.com/Olical/aniseed) *Bridges between fennel and nvim* -->
<!--  - [conjure](https://github.com/Olical/conjure) *Interactive repl based evaluation for nvim* -->
<!--  - [telescope](https://github.com/nvim-telescope/telescope.nvim) *Find, Filter, Preview, Pick* -->
<!--    - [nvim-telescope/telescope-project.nvim](https://github.com/nvim-telescope/telescope-project.nvim) *switch between projects* -->
<!--  - [treesitter](https://github.com/nvim-treesitter/nvim-treesitter) *Incremental parsing system for highlighting, indentation, or folding* -->
<!--  - [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) *Quickstart configurations for the Nvim LSP client* -->
<!--  - [nvim-cmp](https://github.com/hrsh7th/nvim-cmp) *Autocompletion plugin* -->
<!--  - [github-nvim-theme](https://github.com/projekt0n/github-nvim-theme) *Github theme for Neovim* -->
<!--  - [tpope-vim-sexp-bundle](https://github.com/tpope/vim-sexp-mappings-for-regular-people) *sexp mappings for regular people* -->
<!--  - [lualine](https://github.com/nvim-lualine/lualine.nvim) *neovim statusline plugin written in pure lua* -->
<!--  - [luasnip](https://github.com/L3MON4D3/LuaSnip) *Snippet Engine for Neovim written in Lua.* -->
<!--  - [startup](https://github.com/startup-nvim/startup.nvim) *startup themes - using default dashboard* -->
<!-- - [tpope/vim-commentary](https://github.com/tpope/vim-commentary) *toggles a comment for lines, visual selections or for motions* -->
<!-- - [pwntester/octo.nvim](https://github.com/pwntester/octo.nvim) *GitHub Issues & PRs via GitHub CLI* -->
<!-- - [tpope/commentary.vim](https://github.com/tpope/vim-commentary) *toggle line comments* -->
<!-- - [Todo Comments](https://github.com/folke/todo-comments.nvim) *Highlight and search for todo comments (TODO, NOTE, WARNING, FIX, HACK, PERF - specify in options)* -->
<!-- - [neogit](https://github.com/TimUntersberger/neogit) *Magit clone - WIP with lots of useful features already* -->

<!-- Supporting plugins -->
<!-- - https://github.com/folke/trouble.nvim supports Todo Comments -->
<!-- - https://github.com/folke/lsp-colors.nvim -->

<!-- <\!-- TODO: plugins added to configure -\-> -->

<!-- - [] [tpope/fugitive](https://github.com/tpope/vim-fugitive) *Git command line* installed, no key bindings yet (using neogit instead) -->

<!-- <\!-- TODO: plugins to add -\-> -->
<!--  - [ ] [terrortylor/nvim-comment](https://github.com/terrortylor/nvim-comment) -->
<!--  - [ ] [ggandor/leap.nvim](https://github.com/ggandor/leap.nvim) motions (replacement for lightspeed), alternative to easy-motions ?? -->

<!--  - [ ] [kevinhwang91/rnvimr](https://github.com/kevinhwang91/rnvimr) *ranger in a floating window* -->
<!--  - [ ] [dadbod.vim](https://github.com/tpope/vim-dadbod) interact with database - connect `:DB postgresql:///connection-string` or run a single expression -->
<!--  - [ ] [vim-dadbob-ui](https://github.com/kristijanhusak/vim-dadbod-ui) - navigate database connections and save queries -->
<!--  - [ ] [heroku.vim](https://github.com/tpope/vim-heroku) wraps the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) and provides tab complete of commands - https://github.com/tpope/vim-heroku/blob/master/doc/heroku.txt -->
<!--  - [ ] [p00f/nvim-ts-rainbow](https://github.com/p00f/nvim-ts-rainbow) *treesitter based rainbow parens* -->

<!--  - https://github.com/ruifm/gitlinker.nvim share github links -->
