# Customise the shell

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
