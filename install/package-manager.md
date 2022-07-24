# Package Manager

[Packer](https://github.com/wbthomason/packer.nvim) is a [`use-package`](https://github.com/jwiegley/use-package) inspired package management for Neovim.

Packer is used as the package manager in this guide as it is built on native Neovim packages and supports Luarocks dependencies, use the `:help packages` command in Neovim for more details.

Packer is written in Lua and is installed via the `init.lua` configuration file, although Practicalli Neovim configuration uses Fennel to configure each package added by Packer.


## Install

`init.lua` is the entry point to the configuration and is the only part that is written in Lua language.

The configuration bootstraps the Packer package manager and installs the Aniseed compiler required to process the fennel configuration.

Aniseed compiles and loads `fnl/config/init.fnl` and all the required namespaces in that file.

Packer will process the `use` form in `fnl/config/plugin.fnl` and install all the packages defined in that form, along with any package specific configuration defined in that package `{:mod :namespace-name}` file.


```lua

local execute = vim.api.nvim_command
local fn = vim.fn

local pack_path = fn.stdpath("data") .. "/site/pack"
local fmt = string.format

function ensure (user, repo)
  -- Ensures a given github.com/USER/REPO is cloned in the pack/packer/start directory.
  local install_path = fmt("%s/packer/start/%s", pack_path, repo, repo)
  if fn.empty(fn.glob(install_path)) > 0 then
    execute(fmt("!git clone https://github.com/%s/%s %s", user, repo, install_path))
    execute(fmt("packadd %s", repo))
  end
end

-- Bootstrap essential plugins required for installing and loading the rest.
ensure("wbthomason", "packer.nvim")
ensure("Olical", "aniseed")

-- Enable Aniseed's automatic compilation and loading of Fennel source code.
vim.g["aniseed#env"] = {
  module = "config.init",
  compile = true
}
```


## Packages

Neovim packages add extra functionality to Neovim, e.g. conjure package provides an excellent Clojure REPL experience (and supports several other languages too).

See the [packages section](packages/) for details of the packages used and a breakdown of their configuration.
