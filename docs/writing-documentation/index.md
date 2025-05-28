# Writing Documentation

Markdown is a simple and commonly used format for writing documentation.  It can be used to create a project README.md to a complete guide to using the project.


## LSP support

Install [Marksman](https://github.com/artempyanykh/marksman) plugin via Mason to provide anchor link completion.

![Neovim markdown comment with todo comment](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-markdown-marksman-anchor-completion-dark.png?raw=true#only-dark){loading=lazy}
![Neovim markdown comment with todo comment](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-markdown-marksman-anchor-completion-light.png?raw=true#only-light){loading=lazy}


## Static Site Generators

Markdown can be converted into a simple landing page or a fully navigable website.

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) is used by Practicalli to render professional books and blog websites.


## Markdown Syntax

`#` to denote a heading, the number of `#` defines the level of header, one `#` being the largest.

`[name](link-url or #anchor-path)` is the form for an in-page anchor and external URL

`_underline text_` is surrounded by underscore character

`**Bold Text**` is surrounded by double star characters


### Comments

Markdown uses the HTML comment form but with three dashes rather than two.

```markdown
<!--- --->
```

This comment also supports [TODO Comments](/neovim/using-neovim/comments/) in Neovim

```markdown
<!--- TODO: --->
```

![Neovim markdown comment with todo comment](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-markdown-todo-comments-example-dark.png?raw=true#only-dark){loading=lazy}
![Neovim markdown comment with todo comment](https://github.com/practicalli/graphic-design/blob/live/editors/neovim/neovim-markdown-todo-comments-example-light.png?raw=true#only-light){loading=lazy}

!!! HINT "View TODO comments in quicklink buffer"
    `:TODOQuickFix` shows all todos within the current project in the quickfix list, each list item is used to jump to the file and line of that todo.


## Tables

Define the edges of a table with `|` character.  `:-` to separate table column headings and table data.

```markdown
| OS | PATH |
| :- | :--- |
| Linux, MacOS | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |
```
