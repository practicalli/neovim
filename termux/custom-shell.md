# Customise the shell

> Customising the shell is optional, although gives an enhanced experience.

Zsh provides the richest command line experience, providing many advanced features over bash.  The [Prezto configuration](https://github.com/sorin-ionescu/prezto) provides a simple way to configure Zsh features and also supports [powerline10k terminal theme](https://github.com/romkatv/powerlevel10k), providing context specific information and a more engaging visual experience.

## Before installation

Ensure [XDG locations have been set](setup.md) in the `~.profile` file, check with `echo $XDG_CONFIG_HOME` and use `source ~/.profile` if that environment variable is not set.

## Install Zsh
Install the zsh package using the Termux package manager

```
pkg install zsh
```

Start zsh, which will show a `%` character as the prompt

```
zsh
```

## Install Prezto community configuration

Clone prezto and its sub-modules into `XDG_CONFIG_HOME/zsh` which is typically `~/.config/zsh`

```
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-${XDG_CONFIG_HOME:-$HOME/.config}/zsh}/.zprezto"
```


Set the location of the Zsh configuration home with `$ZDOTDIR`, relative to the XDG locations

```
export ZDOTDIR="${ZDOTDIR:=$XDG_CONFIG_HOME/zsh}"
```


Create a new Zsh configuration by copying/linking the Zsh configuration files provided:

```
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

> #### Hint::Practicalli Zsh configuration
> Clone [practicalli/dotfiles](https://github.com/practicalli/dotfiles) and replace the symbolic links in `$XDG_CONFIG_HOME/zsh` with links to the respective Zsh configuration files in the cloned repository (or copy the files if you prefer)
>
> Copy or create a symbolic like for the `.p10k configuration or skip this to create your own configuration when next starting `zsh`.`


Edit `$XDG_CONFIG_HOME/.config/zsh/.zshenv` and add the following lines to enable zsh to find the prezto configuration

```
export XDG_CONFIG_HOME="${XDG_CONFIG_HOME:=$HOME/.config}"
export ZDOTDIR="${ZDOTDIR:=$XDG_CONFIG_HOME/zsh}"
```

Create a symbolic link from `$HOME/.zshenv` to `$XDG_CONFIG_HOME/.config/zsh/.zshenv` (or to the .zshenv file from [practicalli/dotfiles](https://github.com/practicalli/dotfiles))

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

> #### Info::Using Oh My Bash
> If preferring Bash, then [ohmybash](https://ohmybash.nntoan.com/) provides a nice command line experience, showing completions clearer, nice themes that provide information.
