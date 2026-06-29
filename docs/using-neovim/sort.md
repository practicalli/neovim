# Sort lines of text

Neovim has a built-in **`:sort`** command, to sort selected lines of text.

By default lines are sorted in ascending order, although can be sorted in descending order, by numeric values and many other options.

`:help sort` for the built-in documentation.


## All lines

Sort All Lines in the current buffer in ascending order.

```nvim
:%sort
```

## Selected Lines

++shift+"v"++ to visually select one or more lines from the current cursor position.

`:sort` followed by ++enter++ arranges lines in ascending order.

`:sort!` followed by ++enter++ arranges lines in descending order.


## Unique lines


++shift+"v"++ to visually select one or more lines from the current cursor position.

`:sort u` followed by ++enter++ arranges lines in ascending order, removing any duplications.

`:sort! u` followed by ++enter++ arranges lines in descending order, removing any duplications.


> NOTE: `uniq` built-in command also removes duplicate lines adjacent to each other.


## Sort Options

You can customize the sorting behavior with various flags:

- `!`	Sort in descending order
- `u`	unique sort, remove duplicate lines during sort
- `i`	Ignore case during sort
- `n`	Sort by numeric values
- `f`	Sorts by floating-point numbers
- `x`	Sorts by hexadecimal numbers
- `b`	Sorts by binary numbers
- `o`	Sorts by octal numbers


Options n, f,  x, o, and b are mutually exclusive.


## Neovim Plugins


[sQVe/sort.nvim](https://github.com/sQVe/sort.nvim) sorts by delimiters e.g. commas, pipes, colons, etc. Sort strings with numbers, e.g., "item1", "item2", "item10").
