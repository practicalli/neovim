# NeoVim on Termux

A smart phone and an external keyboard can make an excellent ultra-portable development environment, especially when travelling with limited space or restricted weight constraints.

![Ultra-mobile development environment - android with Termux and NeoVim with Keyboardio Atreus keyboard](https://raw.githubusercontent.com/practicalli/graphic-design/live/neovim/ultra-mobile-development--android-termux-neovim-keyboardio-atreus.jpg)

No special permissions are required to set up Termux and installation is made very simple by first installing FDroid marketplace.

## Android app Install

[FDroid](https://f-droid.org/) from Google play store

Open FDroid

Install Termux from F-Droid app store

> NOTE: Termux in Android Play store is out of date and not recommended


## Managing Termux

Termux provides a CLI experience for Linux and the common development tools are easily installed

`pkg` command will add tools and libraries to the Linux environment from the currated packages in the software center.

`apt list --upgradable` shows list of upgradable packages

`apt update` updates the list of packages fromhe software center

`apt upgrade` installs updates for any currently installed packages

`apt-cache search --names-only` - search for packages.

`apt-cache show package-name` - shows detail of package-name, including a description

?? - is package installed


> `pkg` is an alias for `apt`


### Keyboard

Termux provides an extended keyboard with common key bindings for convienience and for combinations not possible with an on-screen keyboard, i.e `Ctrl-c`

For the best experience, especially when a lot of typing is required, plug in a hardware keyboard.  The [Keyboard.io atreus](https://shop.keyboard.io/products/keyboardio-atreus) is an excellent mechanical keyboard that is highly portable.

The on-screen keyboard is swiched off when a hardware keyboard it plugged in, although the extended keyboard is still displayed.

`Volume Up < q` toggles the extended keyboard, so more screen is available when using a hardware keyboard.

> The on-screen keyboard can also be show when a physical keyboard is present, configured in an android setting.


## Tools to download binaries and configuration

* `wget` and `curl` - download tools not packaged, i.e. clojure-lsp binary
* `git` - clone configuration files and projects (see Git version control section)
* `xcopy` - copy file content to the clipboard, e.g. for SSH public key

```
pkg install curl wget git xcopy
```


## byobu terminal window manager

A text window manager in a terminal to run multiple shell tabs, handy for opening multiple terminal sessions for different activities, e.g. Neovim, external Clojure REPL, shell CLI, etc.

```
pkg install byobu
 ```

`F2` to create a new tab
`F3` to select previous tab
`F4` to select next tab

> TODO: configure byobu to run by default (so I dont forget to run it)


## Customise the shell

> Customising the shell is optional, although gives an enhanced experience


Zsh provides advanced features over bash and [Prezto configuration](https://github.com/sorin-ionescu/prezto) provides a simple way to configure these features.  Prezto also supports [powerline10k terminal theme](https://github.com/romkatv/powerlevel10k) that provides context specific information and a more engaging visual experience.

```
pkg install zsh
```
Start zsh

```
zsh
```

Clone prezto and its sub-modules into `~/.config/zsh`

```
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-${XDG_CONFIG_HOME:-$HOME/.config}/zsh}/.zprezto"
```

Configure `$XDG_CONFIG_HOME` and `$ZDOTDIR`

```
export XDG_CONFIG_HOME="${XDG_CONFIG_HOME:=$HOME/.config}"
export ZDOTDIR="${ZDOTDIR:=$XDG_CONFIG_HOME/zsh}"
```
Create a new Zsh configuration by copying/linking the Zsh configuration files provided:
```
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

Edit `$XDG_CONFIG_HOME/.config/zsh/.zshenv` and add the following lines to enable zsh to find the prezto configuration

```
export XDG_CONFIG_HOME="${XDG_CONFIG_HOME:=$HOME/.config}"
export ZDOTDIR="${ZDOTDIR:=$XDG_CONFIG_HOME/zsh}"
```

Create a symbolic link from `$HOME/.zshenv` to `$XDG_CONFIG_HOME/.config/zsh/.zshenv`

```
ln -s $XDG_CONFIG_HOME/.config/zsh/.zshenv $HOME/.zshenv
```

Check the configuration is working by loading the .zshenv configuration

```
source "$ZDOTDIR/.zshenv"
```

Set the shell to run zsh by default

```
chsh -s /data/data/com.termux/files/usr/bin/zsh
```

> #### Info::Using Bash
> [ohmybash](https://ohmybash.nntoan.com/) provides a nice command line experience, showing completions clearer, nice themes that provide information.


## Tools outside packages

Tools such as `clojure-lsp` are not part of the Termux Linux package system and can be downloaded from GitHub releases page via wget or curl

```
pkg install wget curl
```


## Git version control

A Git client is used to version control projects and to clone projects and configuration from GitHub/GitLab.  Practicalli maintains several editor configurations in shared repositories on GitHub

* Install a Git Client (and optionally GitHub CLI)
* [optionally] clone the [practicalli/dotfiles](https://github.com/practicalli/dotfiles) repository for the Git config and global ignores
* Configure an SSH key or Developer token

### Install a git client and GitHub CLI

```
pkg install git gh
```

Clone the [practicalli/dotfiles](https://github.com/practicalli/dotfiles) repository

```
git clone https://github.com/practicalli/dotfiles
```

Move or symbolically link the top-level directories to `~/.config`

Edit the `.config/git/config` and update the user and github / gitlab identities


### Create SSH Key for remote repository access

Install the openssh package which contains the `ssh-keygen` command to generate a new public/private key combinations for use with GitHub SSH repository URLs

```
pkg install openssh
```

Generate a key using the email address of the GitHub or GitLab account

```
ssh-keygen -t rsa -C name@domain.tld
```

RET to confirm storing the password in the default location.

Optionally add a passphrase (recommended), then confirm that passphrase.  Note: the passphrase should be different from the GitHub/GitLab password or your OS login password.

If a passphrase was used to generate the key, add the key to the OpenSSH authentication agent on the Operating System

```bash
ssh-add
```

Vist the GitHub account settings and create a new SSH key

Use `xcopy < ~/.ssh/id_rsa.pub` to copy the public key to the clipboard

Paste the public key into the GitHub new key form


### Create a developer token

A developer token (or ssh key) is required to access GitHub {and far more secure over password}

Should the android device become lost or compromised, the developer token can be deleted to protect the repositories from any malicious access.  The developer token should be limited to the minimal access.  The developer token does not give access to the GitHub or GitLab account.

> HTTPS URLs should be used with a developer token.  git@git.com URLs are for SSH keys only.

Visit GitHub / GitLab settings for your account

Create a new developer token specifically for Termux

Add a descriptive name for the token, based on the device Termuxc is runniung on, e.g. `Termux Pixel2XL`

Check the public_repo and status repo scopes

Generate button creates a new token.

Copy the token using the copy icon.

Edit the `.config/git/config` file and add a github section with the GitHub account name and token

```
[github]
    name = practicalli
    token = ghp_************************************
```

<!-- > TODO: Add a gitlab secion with the same keys if using GitLab -->
<!-- > TODO: How to cache the developer token rather than write it to a file - GitHub CLI -->

> Consider using GitHub CLI to cache the developer token rather than write the token to the Git configuration file for greater security.


## Install neovim
version 7 availabe as current package
```
pkg install neovim
```

## Neovim treesitter
treesitter provides excellent language syntax parsing and highlighting and is a very attractive feature of the recent neovim releases.  Treesitter is a major attraction, bringing in a new audience for Neovim.

### nodejs

```
pkg install nodejs
```


install compiler for neovim-treesitter, to compile some packages

```
pkg install clang
```

> `gcc` is not packaged for Termux, although there are guides to install gcc if preferred. clang seems to be working fine for now though

### Searching files

`SPC f f` to find files to open in Neovim, requires the ripgrep external tool.

```
pkg install ripgrep
```

### install Java

Open JDK install supported, used to host Clojure code

```
pkg install java-17
```

## Install Clojure

Clone practicalli/clojure-deps-edn to add a wide range of community tools to the Clojure CLI

```bash
git clone git@github.com:practicalli/clojure-deps-edn.git ~/.config/clojure
```


Use the Linux install with a prefix path pointing to Termux equivalent of `/usr/local`.  Find the path using `echo $PATH` and remove `bin` from the end.  Without the prefix Clojure will not install correctly

```bash
curl -O https://download.clojure.org/install/linux-install-1.11.1.1124.sh

chmod +x linux-install-1.11.1.1124.sh

./linux-install-1.11.1.1124.sh --prefix /data/data/com.termux/files/usr/
```

`clojure` binary is installed in the existing bin, lib and share directories in `/data/..../usr/`, placing that binary on the system execution path.

Test by running a REPL session, for example with Rebel Readline

```
clojure -M:repl/rebel
```

> optionally install rlwrap package if using the basic repl terminal UI


## Install Clojure LSP

Visit GitHub releases page and download the `clojure-lsp` file
- visit the relases page in firefox and copy the link to the file.
- use wget and paste the link to the file to download
- make executable `chmod 755 clojure-lsp`
- test locally `./clojure-lsp --version` - should print clojure-lsp version and clj-kondo version
- copy or move file to path `mv clojure-lsp $PATH`

If the [practicalli/dotfiles](https://github.com/practicalli/dotfiles) repository was cloned, move or link the `clojure-lsp` directory to `~/.config/clojure-lsp`
