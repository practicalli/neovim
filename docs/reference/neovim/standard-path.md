# Neovim Standard Path

View the standard paths used by Neovim using the help menu

```neovim
:help standard-path
```

Output of command

```neovim
Standard Paths					*standard-path*

Nvim stores configuration, data, and logs in standard locations. Plugins are
strongly encouraged to follow this pattern also. Use |stdpath()| to get the
paths.

                        *base-directories* *xdg*
The "base" (root) directories conform to the XDG Base Directory Specification.
https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
The $XDG_CONFIG_HOME, $XDG_DATA_HOME, $XDG_RUNTIME_DIR, and $XDG_STATE_HOME
environment variables are used if defined, else default values (listed below)
are used.

CONFIG DIRECTORY (DEFAULT) ~
                  *$XDG_CONFIG_HOME*            Nvim: stdpath("config")
    Unix:         ~/.config                   ~/.config/nvim
    Windows:      ~/AppData/Local             ~/AppData/Local/nvim

DATA DIRECTORY (DEFAULT) ~
                  *$XDG_DATA_HOME*              Nvim: stdpath("data")
    Unix:         ~/.local/share              ~/.local/share/nvim
    Windows:      ~/AppData/Local             ~/AppData/Local/nvim-data

RUN DIRECTORY (DEFAULT) ~
                  *$XDG_RUNTIME_DIR*            Nvim: stdpath("run")
    Unix:         /tmp/nvim.user/xxx          /tmp/nvim.user/xxx
    Windows:      $TMP/nvim.user/xxx          $TMP/nvim.user/xxx

STATE DIRECTORY (DEFAULT) ~
                  *$XDG_STATE_HOME*             Nvim: stdpath("state")
    Unix:         ~/.local/state              ~/.local/state/nvim
    Windows:      ~/AppData/Local             ~/AppData/Local/nvim-data

Note: Throughout the user manual these defaults are used as placeholders, e.g.
"~/.config" is understood to mean "$XDG_CONFIG_HOME or ~/.config".

LOG FILE					*$NVIM_LOG_FILE* *E5430*
Besides 'debug' and 'verbose', Nvim keeps a general log file for internal
debugging, plugins and RPC clients. >
    :echo $NVIM_LOG_FILE
By default, the file is located at stdpath('log')/log unless that path
is inaccessible or if $NVIM_LOG_FILE was set before |startup|.
```
