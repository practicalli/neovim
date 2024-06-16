# Notifications

Notification messages are shown in the bottom right corner of Neovim.  Multiple messages are show bottom upwards.

Notifications are set to show for 2 seconds and then are automatically closed.

Notification popups show information, warnings and errors.

![nvim-notify example](https://user-images.githubusercontent.com/24252670/130856848-e8289850-028f-4f49-82f1-5ea1b8912f5e.gif)


## Message History

History of notifications can be browsed to see more detail and to select the text of a notification.

++spc++ ++"f"++ ++"n"++ lists the history of notifications for the current session

++enter++ to open the highlighted item in the list in its own pop-up

++"y"++ ++"y"++ to yank the text of a notification when displayed in a pop-up

![AstroNvim Notifications history](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-notifications-history-light.png?raw=true#only-light){loading=lazy}
![AstroNvim Notifications history](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/astronvim/astronvim-notifications-history-dark.png?raw=true#only-dark){loading=lazy}


!!! INFO "Noice used for notifications UI"
    Practicalli Astro config uses [Noice](https://github.com/folke/noice.nvim) to draw the UI for notification messages, command line and popup menus.


## Configure notifications

Notifications are controlled by [:globe_with_meridians: nvim-notify](https://github.com/rcarriga/nvim-notify)

- `top_down` position of notifications, `false` shows popups from bottom of screen
- `timeout` value controls how long a popup displays, default `3000`
- `level` of information displayed, level 3 hides less important information, e.g. file write messages, default 5

!!! EXAMPLE "Practicalli Astro Configuration for notifications"
    ```lua title="lua/community.lua"
      -- Configure notify popups
      {
        "rcarriga/nvim-notify",
        opts = {
          top_down = false,
          timeout = 2000,
          -- log level - 3 hide file write messages - default 5
          level = 3,
          -- background_color = "#000000",
        },
      },
    ```
