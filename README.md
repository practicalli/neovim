# Practicalli Neovim

```none
██████╗ ██████╗  █████╗  ██████╗████████╗██╗ ██████╗ █████╗ ██╗     ██╗     ██╗
██╔══██╗██╔══██╗██╔══██╗██╔════╝╚══██╔══╝██║██╔════╝██╔══██╗██║     ██║     ██║
██████╔╝██████╔╝███████║██║        ██║   ██║██║     ███████║██║     ██║     ██║
██╔═══╝ ██╔══██╗██╔══██║██║        ██║   ██║██║     ██╔══██║██║     ██║     ██║
██║     ██║  ██║██║  ██║╚██████╗   ██║   ██║╚██████╗██║  ██║███████╗███████╗██║
╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝   ╚═╝   ╚═╝ ╚═════╝╚═╝  ╚═╝╚══════╝╚══════╝╚═╝
```


## Book status

![GitHub issues](https://img.shields.io/github/issues/practicalli/neovim?label=content%20ideas&logo=github)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/practicalli/neovim?label=commits&logo=github)
![GitHub pull requests](https://img.shields.io/github/issues-pr-raw/practicalli/neovim?label=pull%20requests&logo=github)
[![Publish Book](https://github.com/practicalli/neovim/actions/workflows/publish-book.yaml/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/publish-book.yaml)
[![MegaLinter](https://github.com/practicalli/neovim/actions/workflows/megalinter.yml/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/megalinter.yml)


## License and Contributing

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/">
<a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">
<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"></a>
 <a property="dct:title" rel="cc:attributionURL" href="https://github.com/practicalli/neovim">Practicalli Neovim</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://practical.li">Practicalli</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-SA 4.0 </a></p>

Please [read the contributing section of the book](contributing.html) before raising an issue or pull request

By submitting content ideas and corrections you are agreeing they can be used in this workshop under the [Creative Commons Attribution ShareAlike 4.0 International license](https://creativecommons.org/licenses/by-sa/4.0/).  Attribution will be detailed via [GitHub contributors](https://github.com/practicalli/neovim/graphs/contributors).


## Sponsor Practicalli

[![Sponsor practicalli-john](https://raw.githubusercontent.com/practicalli/graphic-design/live/buttons/practicalli-github-sponsors-button.png)](https://github.com/sponsors/practicalli-johnny/)

The majority of my work is focused on the [Practicalli series of books and videos](https://practical.li/) and an advisory role with several communities

Thank you to [Cognitect](https://www.cognitect.com/), [Nubank](https://nubank.com.br/) and a wide range of other [sponsors](https://github.com/sponsors/practicalli-john#sponsors) for your continued support


## GitHub Actions

The megalinter GitHub actions will run when a pull request is created,checking basic markdown syntax.

A review of the change will be carried out by the Practicalli team and the PR merged if the change is acceptable.

The Publish Book GitHub action will run when PR's are merged into main (or the Practicalli team pushes changes to the default branch).

Publish book workflow installs Material for MkDocs version 9


## Local development

Install mkdocs version 9 using the Python pip package manager

```bash
pip3 install mkdocs-material=="9.4"
```

Install the plugins used by the Practicalli site using Pip (these are also installed in the GitHub Action workflow)

```bash
pip3 install mkdocs-material mkdocs-callouts mkdocs-glightbox mkdocs-git-revision-date-localized-plugin mkdocs-redirects pillow cairosvg
```

> pillow and cairosvg python packages are required for [Social Cards](https://squidfunk.github.io/mkdocs-material/setup/setting-up-social-cards/)

Fork the GitHub repository and clone that fork to your computer,

```bash
git clone https://github.com/<your-github-account>/<repository>.git
```

Run a local server from the root of the cloned project

```bash
make docs
```

The website will open at <http://localhost:8000>

If making smaller changes, then only rebuild the content that changes, speeding up the local development process

```bash
make docs-changed
```
