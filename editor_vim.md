# Editor: Vim

Do this chanllege: https://www.shortcutfoo.com/app/dojos/vim

## Cheatsheet

My bad habit:
- Edit at the first of the line: `0i` **->** `I`
- `t` and `f` is different: `t` is to **before the character** where `f` **includes the character**. That's why when you copy to quote you should use `vf'` instead of `vt'` (this will miss the last character before `'`)
- Move to first non whitespace char: `0w` **->** `^`

Good to use:
- Go to line number 12: `12G`
- `H/M/L` Move to first/middle/last line of screen


Good to know:
- move screen: `CTRL+e` or `CTRL+y`
- `:x` is same as `:wq`
