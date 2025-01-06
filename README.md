# base16-nvim

Originally, this was a Lua port of [chriskempson/base16-vim](https://github.com/chriskempson/base16-vim) for [Neovim](https://github.com/neovim/neovim). As base16-vim now appears to be abandonware, the new upstream is considered to be [tinted-vim](https://github.com/tinted-theming/tinted-vim) (itself, a fork of base16-vim).

## Why?

These schemes are implemented in pure Lua, using the lowest-level API for creating highlight groups ([`vim.api.nvim_set_hl`](https://neovim.io/doc/user/api.html#nvim_set_hl())), so as to have the minimum possible impact on startup time.
