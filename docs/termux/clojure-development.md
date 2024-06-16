# Clojure development environment

A comprehensive development environment for Clojure, supporting a REPL workflow and static analysis of code via Clojure Language Server Protocol.


## Java host platform

Install OpenJDK to host the Clojure REPL process and run packaged Clojure applications.

Java 17 Long Term Support version is recommended as it is very stable, receives security updates and has the latest highly tested performance improvements.

```
pkg install openjdk-17
```

<!-- TODO: Install openjdk-21 when it has been packaged for Termux -->


## Install Clojure

Clone practicalli/clojure-deps-edn to add a wide range of community tools to the Clojure CLI

```bash
git clone git@github.com:practicalli/clojure-deps-edn.git ~/.config/clojure
```


Use the Linux install with a prefix path pointing to Termux equivalent of `/usr/local`.  Find the path using `echo $PATH` and remove `bin` from the end.  Without the prefix Clojure will not install correctly

```bash
curl -L -O https://github.com/clojure/brew-install/releases/latest/download/linux-install.sh && \
chmod +x linux-install.sh && \
./linux-install.sh --prefix /data/data/com.termux/files/usr/
```

`clojure` binary is installed in the existing bin, lib and share directories in `/data/..../usr/`, placing that binary on the system execution path.

Test by calling `clojure` with the --help option, which shows the options available to the command

```shell
clojure --help
```

Run a Clojure REPL session from a Clojure project configured with a `deps.edn` file

```shell
clojure -M:repl/rebel
```

> optionally install rlwrap package if using the basic REPL terminal UI with the `clj` wrapper script


## Install Clojure LSP

Visit [clojure-lsp GitHub releases page](https://github.com/clojure-lsp/clojure-lsp/releases){target=_blank} and download the `clojure-lsp` file

- visit the relases page in firefox and copy the link to the file.
- use wget and paste the link to the file to download
- make executable `chmod 755 clojure-lsp`
- test locally `./clojure-lsp --version` - should print clojure-lsp version and clj-kondo version
- copy or move file to path `mv clojure-lsp $PATH`

If the [practicalli/clojure-lsp-config](https://github.com/practicalli/clojure-lsp-config){target=_blank} repository was cloned, move or link the `clojure-lsp` directory to `~/.config/clojure-lsp`
