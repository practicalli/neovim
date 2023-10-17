# Notifications

??? INFO "Notifications only in AstroNvim, not the Practicalli Neovim configuration"

++spc++ ++"f"++ ++"n"++ lists the history of notifications for the current sesion

++enter++ to open the highlighted item in the list in its own popup


Notification popups show information, warnings and errors.

![nvim-notify example](https://user-images.githubusercontent.com/24252670/130856848-e8289850-028f-4f49-82f1-5ea1b8912f5e.gif)


## Configure notifications

Notifications are controlled by [:globe_with_meridians: nvim-notify](https://github.com/rcarriga/nvim-notify)

[:fontawesome-solid-book-open: Practicalli astronvim-config](https://practical.li/neovim/configuration/astronvim/#clone-astronvim-user-config) overrides several default values in `plugins/core.lua`

- `top_down` position of notifications, `false` shows popups from bottom of screen
- `timeout` value controls how long a popup displays, defautl `3000`
- `level` of information displayed, level 3 hides less important information, e.g. file write messages, default 5

!!! EXAMPLE "Practicalli Configuration for notifications"
    ```lua title="plugins/core.lua"
      -- Configure notify popups
      {
        "rcarriga/nvim-notify",
        opts = {
          top_down = false,
          timeout = 1000,
          -- log level - 3 hide file write messages - default 5
          level = 3,
          -- background_color = "#000000",
        },
      },
    ```


!!! INFO "Noice uses nvim-notify configuration"
    [Noice](https://github.com/folke/noice.nvim) replaces the UI for messages, command line and popup menus, although uses the configuration of nvim-notify for position and popup timing.

