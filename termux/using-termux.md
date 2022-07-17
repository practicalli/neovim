# Using Termux

Termux provides a Linux command line experience, providing a wide range of Unix tools and development environments.  Termux uses a Debian based system and packages are easily installed

* `apt install` add tools and libraries to the Linux environment from the curated packages in the software center
* `apt update` updates the list of packages fromhe software center
* `apt list --upgradable` shows list of packages with new versions
* `apt upgrade` install new versions of currently installed packages
* `apt-cache search --names-only` - search for packages that include a specific pattern in their name.
* `apt-cache show` - shows detail of the supplied package name, including a description

> `pkg` is an alias for `apt`, the advance package tool, although there seems little benefit to using pkg if familiar with apt (they are both 3 characters)


## Software Keyboard

Termux provides an extended keyboard with common key bindings for convienience and for combinations not possible with an on-screen keyboard, i.e `Ctrl-c`

For the best experience, especially when a lot of typing is required, plug in a hardware keyboard.  The [Keyboard.io atreus](https://shop.keyboard.io/products/keyboardio-atreus) is an excellent mechanical keyboard that is highly portable.

The on-screen keyboard is swiched off when a hardware keyboard it plugged in, although the extended keyboard is still displayed.

`Volume Up + q` toggles the extended keyboard, so more screen is available when using a hardware keyboard.

> The on-screen keyboard can also be show when a physical keyboard is present, configured in an android setting.



## Byobu terminal tab manager

Termux provides a single terminal prompt. Byobu provides multiple shell prompts, allowing individual Clojure tools and editors to be run from the Termux prompt simultaneously.  Practicalli uses byobu to run Neovim, a Clojure REPL and unit test watcher in separate byobu tabs with the ability to add further tabs for other command line tools.

```
pkg install byobu
```

* `F2` to create a new tab
* `F3` to select previous tab
* `F4` to select next tab

`byobu-enable` command will configure the current shell to run byobu on startup.  Test this is working by typing `exit` in Termux and start Termux app again. `byobu-disable` stops this behaviour and byobu will need to be run manually after starting Termux.

> Run the `byobu-enable` command again if zsh is configured after this step or if adding any other shell to Termux.
