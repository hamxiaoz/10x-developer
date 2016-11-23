# SublimeText

## Packages
My preferences and used packages: https://github.com/hamxiaoz/my-scripts

- vim ex mode: http://www.sublimetext.com/docs/2/vintage.html 
- git gutter: https://github.com/jisaacks/GitGutte
- sidebarenhancement

The following looks good but not tested
- https://github.com/vkocubinsky/SublimeTableEditor
- https://github.com/noklesta/SublimeQuickFileCreator
- https://github.com/twolfson/FindPlusPlus
- https://github.com/dzhibas/SublimePrettyJson

## Theme
[Monokai-Soda](https://github.com/hamxiaoz/Monokai-Soda-hamxiaoz)

## Setup

#### How to have an "Open with sublime" icon in Finder toolbar? 
![](/img/sublime-open-folder-from-toolbar.gif)
Go to my repo [open-folder-with-sublime](https://github.com/hamxiaoz/open-folder-with-sublime) and follow the instructions.

#### How to open current folder in command line?
- do this [setup](Open current folder in command line, do this [setup](x)
- then you can use like this: `subl .`


---

## Shortcuts/Tips

http://www.cheatography.com/ducondez/cheat-sheets/core-sublimetext/

### Pane Management
- `ALT+CMD+num`: open number of panes
- `CTRL+num`: switch to pane
- `CTRL+SHIT+num`: move tab to pane

Inside pane:
- `CMD+1/2/3`: go to tab, most avtive to tabs
- `SHIFT+CMD+[/]`: go to next tab

Use Origami: `super+k` to start:
- `super+z` to zoom, `shift+super+z` to reset
- use arrow to switch to panes
  - press `shift` to carry file.
  - press `alt` to clone file.


### Selections / Multiple line editing
`CMD+D` 
- select the whole word even you're in the middle
- hit multiple times will add up selections (multiple edit)

`CMD+G`: find next (cmd+D first), similar to it but it has visual

`CTRL+CMD+G`: select all current highlight

`CMD+SHIFT+L`: **split lines** in selection, then v to exit visual mode

`SHIFT+CMD+SPACE`: select parent scope, can I do it in vintage without telling the parent?


#### Search
symbol search in ST3



---

### Editing Tips

#### How to remove the bullet points '1./2./3.' for multiple lines?
Old way in vim: line by line.
- delete on 1st line then j0.
- or q to record to 1 then 10@1

New way in vim/ST: multiple line editing:
- select all lines
- split lines selection: `SHIFT+CMD+L`
- v to exit v mode then 0dw

Example:

```
# FROM:
- US Patent No. 4,136,359: "Microcomputer for use with video display"[41]—for which he was inducted into the National Inventors Hall of Fame.
- US Patent No. 4,210,959: "Controller for magnetic disc, recorder, or the like"[42]
- US Patent No. 4,217,604: "Apparatus for digitally controlling PAL color display"[43]
- US Patent No. 4,278,972: "Digitally-controlled color signal generation means for use with display"[44]

# TO:
US Patent No. 4,136,359: "Microcomputer for use with video display"[41]—for which he was inducted into the National Inventors Hall of Fame.
US Patent No. 4,210,959: "Controller for magnetic disc, recorder, or the like"[42]
US Patent No. 4,217,604: "Apparatus for digitally controlling PAL color display"[43]
US Patent No. 4,278,972: "Digitally-controlled color signal generation means for use with display"[44]

# answer (with vi mode): V -> } -> CMD+SHIFT+L -> v -> 0 -> dw -> ESC
```
