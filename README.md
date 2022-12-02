## Book status

![GitHub issues](https://img.shields.io/github/issues/practicalli/neovim?label=content%20ideas&logo=github) 
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/practicalli/neovim?label=commits&logo=github) 
![GitHub pull requests](https://img.shields.io/github/issues-pr-raw/practicalli/neovim?label=pull%20requests&logo=github)
[![GitBook publish](https://github.com/practicalli/neovim/actions/workflows/publish-book.yml/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/publish-website.yaml) 
[![MegaLinter](https://github.com/practicalli/neovim/actions/workflows/megalinter.yml/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/megalinter.yml) 


## License and Contributing

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/">
<a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">
<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"></a>
 <a property="dct:title" rel="cc:attributionURL" href="https://github.com/practicalli/neovim">Practicalli Neovim</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://practical.li">Practicalli</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-SA 4.0 </a></p>

Please [read the contributing section of the book](contributing.html) before raising an issue or pull request

By submitting content ideas and corrections you are agreeing they can be used in this workshop under the [Creative Commons Attribution ShareAlike 4.0 International license](https://creativecommons.org/licenses/by-sa/4.0/).  Attribution will be detailed via [GitHub contributors](https://github.com/practicalli/neovim/graphs/contributors).


## GitHub Actions

The megalinter GitHub actions will run when a pull request is created,checking basic markdown syntax.

A review of the change will be carried out by the Practicalli team and the PR merged if the change is acceptable.

The Publish Book GitHub action will run when PR's are merged into main (or the Practicalli team pushes changes to the default branch).


## Local development

Install mkdocs using the Operating system package manager

```bash
sudo apt install mkdocs
```

Or via Python pip

```bash
pip install mkdocs
```

Install the plugins used by the Practicalli site using Pip (these are also installed in the GitHub Action workflow)

```bash
pip install mkdocs-material mkdocs-callouts mkdocs-glightbox mkdocs-git-revision-date-localized-plugin
```

Fork the practicalli/neovim GitHub repository and clone that fork to your computer,

```bash
git clone https://github.com/<your-github-account>/neovim.git

```

Run a local server from the root of the cloned project

```bash
mkdocs serve
```

The website will open at http://localhost:8000
