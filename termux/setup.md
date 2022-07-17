# Termux Setup

Launch Termux via its application icon.  A black terminal screen will appear with a bash shell prompt.


## Update packages

Check for new packages and update them all

```
package upgrade -y
```

If you wish to first check the packages that will be updated, use `pkg --list-upgradable`

`termux-change-repo` to select a specific region to minimise the number of mirrors checked during package upgrades, especially useful if on a limited data plan.

> At time of writing, the Termux package on F-Droid was around 6 months old so there will be a number of packages that should be updated before any further installation steps are undertaken.


## Configure Freedesktop.org XDG locations

`nano ~/.profile` to edit the `~/.profile` file, adding export directives to set the XDG locations:

```bash
export XDG_CONFIG_HOME=$HOME/.config
export XDG_DATA_HOME=$HOME/.local/share
export XDG_STATE_HOME=$HOME/.local/state
export XDG_CACHE_HOME=$HOME/.cache

# Set XDG location of Emacs Spacemacs configuration
export SPACEMACSDIR="$XDG_CONFIG_HOME/spacemacs"
```

`source ~/.profile` to load the environment variables into the shell, or exit Termux and restart.


## Tools to download binaries and configuration

Many tools can be installed via the `pkg` tool, although specific Clojure tools and configuration require additional tools:

* `wget` and `curl` - download tools not packaged, i.e. clojure-lsp binary
* `git` - clone configuration files and projects (see Git version control section)
* `openssh` - SSH service and tools to generate SSH keys

```
pkg install curl wget git openssh
```

[Configure a Git Identify and SSH key](git-version-control.md) to make full use of the Git client.  [practicalli/dotfiles](https://github.com/practicalli/dotfiles) contains example configuration, ignore patterns and commit template.

## [Optional] Configure Termux Settings

`nano ~/.termu/termux.properties` to configure the default settings for termux.

`termux-reload-settings` if any of the values are set (restarting Termux is not enough to load setting changes)

The defaults are suitable for the majority of uses, although you may wish to consider:

* `hide-soft-keyboard-on-startup` set to true if always using a physical keyboard or to have more screen space by default
* `default-working-directory` to save files in an alternative location, e.g. SD storage



## Set Color Scheme and Font

If the Termux:Styling plug was installed via F-Droid, then Termux colors and fonts can be customised easily.

Press and hold on the Termux screen to show the copy/paste menu and select the **Style** menu.  On smaller screens select **More > Style**

A menu appears with **Choose Color** and **Choose Font**

Select **Choose Color** to select from the available list of colour schemes, e.g. Gruvbox Dark or Gruvbox Light

Select **Choose Font** to select from the available fonts, e.g. FiraCode or Ubuntu
