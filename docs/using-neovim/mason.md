# Mason

Manage packages for LSP servers, format & lint tools from within Neovim.

++spc++ ++"p"++ ++"m"++ opens the Mason status,

- ++"i"++ to install package under cursor
- ++"U"++ to update all packages.
- ++"X"++ to remove package under cursor

The [Mason Registry](https://mason-registry.dev/registry/list){target=_blank} maintains a list of all packages and automatically updated packages to the latest available version.

[Mason Registry - Package List](https://mason-registry.dev/registry/list){target=_blank .md-button}

!!! TIP "SPC p a updates plugins and tools"

![Mason status](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim-5/nvim-tools-mason-status.png?raw=true){loading=lazy}


## Help

++"g"++ ++"?"++ on Mason status popup shows key maps and description of mason

`:checkhealth mason` health status of mason

`:help mason-debugging` for help with debugging

![Mason help](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim-5/neovim-tools-mason-help.png?raw=true){loading=lazy}

??? EXAMPLE "Mason Log"
    ```shell-session
    [INFO  Wed 02 Apr 2025 15:40:41 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=lua-language-server) {}
    [INFO  Wed 02 Apr 2025 15:40:41 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=stylua) {}
    [INFO  Wed 02 Apr 2025 15:40:41 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=selene) {}
    [INFO  Wed 02 Apr 2025 15:40:41 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=clojure-lsp) {}
    [INFO  Wed 02 Apr 2025 15:40:43 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=stylua)
    [INFO  Wed 02 Apr 2025 15:40:44 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=lua-language-server)
    [INFO  Wed 02 Apr 2025 15:40:44 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=selene)
    [INFO  Wed 02 Apr 2025 15:40:48 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=clojure-lsp)
    [INFO  Mon 07 Apr 2025 22:43:03 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=json-lsp) {}
    [INFO  Mon 07 Apr 2025 22:43:08 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=json-lsp)
    [INFO  Thu 10 Apr 2025 11:14:42 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=gh-actions-language-server) {}
    [INFO  Thu 10 Apr 2025 11:14:51 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=gh-actions-language-server)
    [INFO  Mon 14 Apr 2025 21:00:36 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=lua-language-server) {
      version = "3.14.0"
    }
    [INFO  Mon 14 Apr 2025 21:00:39 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=lua-language-server)
    [INFO  Thu 24 Apr 2025 10:09:44 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=clojure-lsp) {
      version = "2025.04.23-18.16.46"
    }
    [INFO  Thu 24 Apr 2025 10:09:44 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=stylua) {
      version = "v2.1.0"
    }
    [INFO  Thu 24 Apr 2025 10:09:46 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=stylua)
    [INFO  Thu 24 Apr 2025 10:09:49 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=clojure-lsp)
    [INFO  Thu 24 Apr 2025 10:39:26 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=clojure-lsp) {
      version = "2025.03.27-20.21.36"
    }
    [ERROR Thu 24 Apr 2025 10:39:30 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:249: Installation failed for Package(name=clojure-lsp) error="Installation was aborted."
    [INFO  Thu 01 May 2025 21:15:13 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=marksman) {}
    [INFO  Thu 01 May 2025 21:15:13 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:184: Executing installer for Package(name=prettierd) {}
    [INFO  Thu 01 May 2025 21:15:15 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=marksman)
    [INFO  Thu 01 May 2025 21:15:18 BST] ...astro5/lazy/mason.nvim/lua/mason-core/installer/init.lua:245: Installation succeeded for Package(name=prettierd)
    [ERROR Sun 20 Apr 2025 20:00:55 BST] ...astro5/lazy/mason.nvim/lua/mason-core/providers/init.lua:81: Provider "github" "get_latest_release" failed: spawn: wget failed with exit code 5 and signal 0.
    ```
