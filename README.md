# base16-nvim

A Lua port of [base16-vim](https://github.com/chriskempson/base16-vim) for [Neovim](https://github.com/neovim/neovim).

## Update procedure

In order to always be testing the latest and greatest version of these color schemes, I add this repo as a submodule to [my dotfiles repository](https://github.com/wincent/wincent), and work out of there. [The script for actually rebuilding schemes](https://github.com/wincent/wincent/blob/main/support/base16-builder.rb) is stored in the superproject.

### Tracking upstream template updates

Examples of "backports" of changes made in [base16-vim](https://github.com/chriskempson/base16-vim):

- [d2b7bbadebf666c2](https://github.com/wincent/base16-nvim/commit/d2b7bbadebf666c2a2e9e9410c009774554f5249).
- [e17c89c913d5ef91](https://github.com/wincent/base16-nvim/commit/e17c89c913d5ef9177452636e0b81311a8481a99).
- [3e732be2af2b6282](https://github.com/wincent/base16-nvim/commit/3e732be2af2b62822826aa95a9e2d77a735356be).

The basic pattern is:

1.  Make the changes to [the `templates/default.mustache` template](templates/default.mustache) in this repo (ie. in the submodule). This requires a decision for how to port the Vimscript of each upstream change into Lua.

2.  Copy the new template up to the superproject's working area by running this (from the superproject root):

    ```
    cp \
      aspects/nvim/files/.config/nvim/pack/bundle/opt/base16-nvim/templates/default.mustache \
      vendor/base16-templates/base16-nvim/templates
    ```

3.  Run `NO_CLONE=1 support/base16-builder.rb` in the superproject. The `NO_CLONE` stops the changed template that was copied in the previous step from being updated.

4.  Commit the changes in the base16-nvim submodule:

    ```
    cd aspects/nvim/files/.config/nvim/pack/bundle/opt/base16-nvim
    git commit -p
    git push
    cd -
    ```

4.  Produce a dotfiles commit (example: [d0da206692f96e19](https://github.com/wincent/wincent/commit/d0da206692f96e19552343a938f1686b37b1f36d)):

    ```
    git add aspects/nvim/files/.config/nvim/pack/bundle/opt/base16-nvim
    git commit
    ```

5.  Clean up the working area in the superproject:

    ```
    cd vendor/base16-templates/base16-nvim
    git fetch
    git reset --hard origin/main
    cd -
    ```

### Tracking upstream scheme updates

Examples of updating when new schemes are added, or existing schemes changed, upstream:

- [92ed876c7ded75f7](https://github.com/wincent/base16-nvim/commit/92ed876c7ded75f7e8ef63927aca2616e90af50d).

These updates are straightforward:

1.  In [my dotfiles](https://github.com/wincent/wincent), update the list of templates and the list of schemes:

    ```
    (cd vendor/base16-templates-source && git pull)
    (cd vendor/base16-schemes-source && git pull)
    ```

2.  Run [`support/base16-builder.rb`](https://github.com/wincent/wincent/blob/main/support/base16-builder.rb).

3.  Commit the changes in my base16-nvim submodule:

    ```
    cd aspects/nvim/files/.config/nvim/pack/bundle/opt/base16-nvim
    git commit -p
    git push
    cd -
    ```

4.  Produce a dotfiles commit (example: [7b26cdbf8ee35459](https://github.com/wincent/wincent/commit/7b26cdbf8ee35459aa6c8d553c449e99e07d78ec)):

    ```
    git add aspects/nvim/files/.config/nvim/pack/bundle/opt/base16-nvim
    git add vendor/base16-{templates,schema}-source
    git commit
    ```
