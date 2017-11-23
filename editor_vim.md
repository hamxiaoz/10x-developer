# Editor: Vim

Do this chanllege: https://www.shortcutfoo.com/app/dojos/vim

## Cheatsheet (that I don't know)

My bad habit (mostly motion):
- use `3j` or `3k` instead of hitting `jjjj` or `kkkk`
- Edit at the first of the line: `0i` **->** `I`
- Move to first non whitespace char: `0w` **->** `^`
- Navigation in current screen: `H/M/L` first/middle/last
- Scroll current line to top of window: `zt`
- `t` and `f` is different: `t` is to **before the character** where `f` **includes the character**. That's why when you copy to quote you should use `vf'` instead of `vt'` (this will miss the last character before `'`)

Good to use:
- Good to navigate based on error message:
  - Go to line number 12: `12G`
  - Go to column 20: `20l`
- Go to previous location: <code>``</code> (two backticks)
- Use bookmark: `ma` (mark with a) then <code>`a</code> (go to a)

Good to know:
- Swap case: `~` (can do it in normal mode)
- move screen: `CTRL+e` or `CTRL+y`
- `:x` is same as `:wq`


## Cheatsheet
- `%`
- `gu` `gU`
- `*` `n` `N`
