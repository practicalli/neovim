# Terminal

[akinsho/toggleterm.nvim](https://github.com/akinsho/toggleterm.nvim) plugin provides a terminal session within Neovim, using a float, split or tab.


++spc++ ++"t"++ for the Terminal sub-menu 

++spc++  ++"t"++ ++"f"++ opens a terminal in a floating window, useful for one-off commands or short sessions

++spc++  ++"t"++ ++"f"++ opens a terminal in a horizontal split, useful for a process that prints valuable feedback, e.g. a test runner in watch mode

`:Toggleterm direction=tab` opens a terminal in a tab page, useful for long running processes

<!-- TODO: Add key binding for Terminal in a tab to lua/plugins/user-practicalli.lua -->

![Toggleterm.nvim float](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-terminal-float-directory-listing-light.png?raw=true#only-light){loading=lazy}
![Toggleterm.nvim float](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/screenshots/neovim-terminal-float-directory-listing-dark.png?raw=true#only-dark){loading=lazy}
