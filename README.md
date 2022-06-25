## Book status

[![GitHub issues](https://img.shields.io/github/issues/practicalli/neovim?label=content%20ideas&logo=github)](https://img.shields.io/github/issues/practicalli/neovim?label=content%20ideas&logo=github) [![GitHub commit activity](https://img.shields.io/github/commit-activity/y/practicalli/neovim?label=commits&logo=github)](https://img.shields.io/github/commit-activity/y/practicalli/neovim?label=commits&logo=github) [![GitHub pull requests](https://img.shields.io/github/issues-pr-raw/practicalli/neovim?label=pull%20requests&logo=github)](https://img.shields.io/github/issues-pr-raw/practicalli/neovim?label=pull%20requests&logo=github) [![GitBook publish](https://github.com/practicalli/neovim/actions/workflows/publish-website.yaml/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/publish-website.yaml) [![MegaLinter](https://github.com/practicalli/neovim/actions/workflows/megalinter.yml/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/megalinter.yml) [![pages-build-deployment](https://github.com/practicalli/neovim/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/practicalli/neovim/actions/workflows/pages/pages-build-deployment)

## License and Contributing

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/">
<a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">
<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"></a>
 <a property="dct:title" rel="cc:attributionURL" href="https://github.com/practicalli/neovim">Practicalli Neovim</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://practical.li">Practicalli</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-SA 4.0 </a></p>

Please [read the contributing section of the book](contributing.md) before raising an issue or pull request

By submitting content ideas and corrections you are agreeing they can be used in this workshop under the [Creative Commons Attribution ShareAlike 4.0 International license](https://creativecommons.org/licenses/by-sa/4.0/).  Attribution will be detailed via [GitHub contributors](https://github.com/practicalli/neovim/graphs/contributors).

### GitHub Actions

The megalinter GitHub actions will run when a pull request is created,checking basic markdown syntax.

A review of the change will be carried out by the Practicalli team and the PR merged if the change is acceptable.

The Publish Website GitHub action will run when PR's are merged (or the Practicalli team pushes changes to the default branch).

## GitBook Static Site Generator

[GitBook open source tool](https://github.com/GitbookIO/gitbook) is used to generate all the Practicalli books, as it provides a simple way to provide effective navigation across a guide or book with a large number of pages.

### Install locally

GitBook can be installed locally to support larger pieced of content development.  It provides a local server that should continually build the site when changes are saved.

GitBook requires [node.js version 11](https://nodejs.org/dist/latest-v11.x/) (or version 10, or 8)

Install GitBook using node package manager

```bash
npm install gitbook-cli -g
```

Fork the practicalli/clojure GitHub repository and clone that fork to your computer,

```bash
git clone https://github.com/<your-github-account>/clojure.git

```

Install the GitBook plugins used for this project (as defined in the [book.json](book.json) configuration)

switch to the root directory of the cloned repository when complete.

```bash
gitbook install
```

> If any plugins fail to install, ensure node version 11 (or 10) is being used

Run a local server to generate the website from the markdown content, which also listens for changes

```bash
gitbook serve
```

### Gitbook plugins

[GitBook has numerous community plugins](https://www.npmjs.com/search?q=gitbook%20plugin) to extend its functionality.

The following plugins are currently used for Practicalli books.

* [anchor-headings-lambda](https://www.npmjs.com/package/gitbook-plugin-anchor-headings-lambda)
* [callouts](https://www.npmjs.com/package/gitbook-plugin-callouts)
* [codeblock-disable-glossary](https://www.npmjs.com/package/gitbook-plugin-codeblock-disable-glossary)
* [disqus](https://github.com/GitbookIO/plugin-disqus)
* [folding-chapters](https://www.npmjs.com/package/gitbook-plugin-folding-chapters-2) - fold navigation sections
* [ga](https://www.npmjs.com/package/gitbook-plugin-ga) - Google analytics
* -glossary - disable default glossary
* [-highlight](https://www.npmjs.com/package/gitbook-plugin-highlight) - disable default highlight (prism)
* [klipse](https://www.npmjs.com/package/gitbook-plugin-klipse) - embed Klipse code evaluation in pages
* [newtabs](https://www.npmjs.com/package/gitbook-plugin-newtabs) - in-page tab sections
* [prism](https://www.npmjs.com/package/gitbook-plugin-prism) code block syntax highlighting (use jr0cket.css theme, added manually)
* [sectionx-ex](https://www.npmjs.com/package/gitbook-plugin-sectionx-ex) - in-page sections that can be collapsed (klipse doesnt work inside a section)
* [-sharing](https://www.npmjs.com/package/gitbook-plugin-sharing)  - buttons to share on social media (default plugin disabled)
* [splitter](https://www.npmjs.com/package/gitbook-plugin-splitter) - movable vertical bar between navigation and content, remembers position
* [terminull-light](https://www.npmjs.com/package/gitbook-plugin-terminull-light) - fancy console - draws copy button on klipse elements
* [theme-jr0cket](https://www.npmjs.com/package/gitbook-plugin-theme-jr0cket) - custom version of theme-code, removing numbering
* [toggle-chapters](https://www.npmjs.com/package/gitbook-plugin-toggle-chapters) - collapsed and expand navigation sections
* [toolbar](https://www.npmjs.com/package/gitbook-plugin-toolbar) - add toolbar of links to GitHub, Chat, etc.
* [youtubex](https://www.npmjs.com/package/gitbook-plugin-youtubex) - embed YouTube videos by id, rending responsively to page size
* [wide-page](https://github.com/ingoclaro/gitbook-plugin-wide-page) - gitbook plugin to have a fluid page width instead of fixed
