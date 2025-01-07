# Folding

Folding

Focus on the most important part of a buffer or file by folding source code and other text that is not currently needed.


++"z"++  menu has key mappings to control folds

++"z"++ ++"a"++ toggle current fold is very convenient for unfolding and folding the last fold.


There are six methods to select folds:

- manually define folds
- more indent means a higher fold level
- specify an expression to define folds
- folds defined by syntax highlighting
- diff folds for unchanged text
- folds defined by markers in the text


!!! INFO "fold docs"
    ```
    :help fold
    ```

[Fold - Neovim docs](https://neovim.io/doc/user/fold.html){target=_blank .md-button}


## objects


++"z"++ ++"f"++ ++"a"++ ++"("++ wraps around matching parentheses ?



## Motions




## Treesitter folding

Fold using Treesitter based text objects.

++"z"++ ++"a"++ will toggle the fold for the current treesitter text object, e.g folds the top level expression that contains the cursor.

Specific text objects can be specified

++"z"++ ++"f"++ ++"a"++ ++"f"++ fold around top-level form at cursor




TODO: fold with markers
