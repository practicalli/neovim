# Language Providers

Neovim delegates some features to [language providers](https://neovim.io/doc/user/provider.html){target=_blank}.

`:checkhealth` command in Neovim shows if the binaries and tools required by each provider are available in the operating system.

Resolve the issue with providers that generate a warning in the checkhealth report, following the ADVICE steps provided.


## Disable Language Providers

If a language is not used with Neovim, then its provider can be disabled.  Details on how to disable a provider are included at the end of the ADVICE in the report section for that provider.

![NeoVim checkhealth report - python provider warning](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/screenshots/neovim-checkhealth-warning-python.png)

Disable language providers in the `init.lua` configuration file

```lua title="init.lua"
-- Disable Language providers
vim.g.loaded_node_provider = 0       --- (1)!
vim.g.loaded_perl_provider = 0
vim.g.loaded_python3_provider = 0
vim.g.loaded_ruby_provider = 0
```

1.  Example configuration to disable providers is provided in the [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux){target=_blank} configuration


!!! TIP "Ignore Language Provider warnings"
    If the programming language is not used, there are no issues with using Neovim if the warnings are simply ignored
