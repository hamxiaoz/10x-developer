# Editor: VS Code

- [ ] intro
- [ ] Editor
- [ ] Customization


_ [Everything git](https://github.com/Microsoft/vscode-tips-and-tricks#task-runner)

_ custom snippets

## HTML with Emmet
http://code.visualstudio.com/docs/languages/html#_emmet-snippets

## Task
A task is shortcut to run external action (grunt, shell) without leaving your editor, such as build, test, etc.

To use, press `CMD+P` and type: `task TASK_NAME`.

Sample task:

```
{
    "version": "0.1.0",
    "tasks": [
        {
          "taskName": "ks",
          "command": "killall",
          "args": ["-9", "grunt"],
          "isShellCommand": true,
          "suppressTaskName": true,
          "showOutput": "never"
        }
    ]
}
```

## Debug
You can press `F5` to debug any single file.


## Hotkeys

Sidebar
- Toggle side pane: `CMD+B`

Explorer:
- Switch to file pane: `SHIFT+CMD+E` (How to remember? Same hotkey prefix for find: `SHIFT+CMD+F`)
- Open file in next pane: Hold `CMD` while click the file or `CMD+ENTER`

Search:
- Swith to the search pane: `SHIFT+CMD+F` (simialr to Explorer pane: `SHIFT+CMD+E`)
- Switch search history: `ALT+UP/DOWN`
- Path glob pattern:
  ```
  Click on the toggle to the right to enable the glob pattern syntax:

  * to match one or more characters in a path segment
  ? to match on one character in a path segment
  ** to match any number of path segments, including none
  {} to group conditions (e.g. {**/*.html,**/*.txt} matches all HTML and text files)
  [] to declare a range of characters to match (e.g., example.[0-9] to match on example.0, example.1, …)
  ```

Navigation in Editor
- Switch editors p 1/2/3: `CMD+1/2`
- in `CMD+P` Quick Open list, hit enter to open in current pane, hit `CMD+\` to open in next pane.
- Move active editor to left/right group: `CTRL+CMD+LEFT/RIGHT`
  
  ```
  { "key": "ctrl+cmd+right",        "command": "workbench.action.moveEditorToNextGroup" },
  { "key": "ctrl+cmd+left",         "command": "workbench.action.moveEditorToPreviousGroup" }
  ```
- Switching files inside on editor: `SHIFT+ALT+TAB`  

Editing
- Show IntelliSense: `CTRL+SPACE`
- Find by symbol (instead of find by text): `CMD+SHIFT+O` (When viewing JSON file, it'll find by the key)
- File navigation:
  - Show list of files in one editor or go back and forth between files: `CTRL+TAB`
  - `CTRL+-` to go back last file
  - to last position: `CMD+U`
- Code reformatting: `CMD+K, CMD+F`
- Code folding: `SHIFT+CMD+[ or ]`
- Trim trailing whitespace: `CMD+SHIFT+X`

Terminal: "ctrl+`"

### Custom Hotkeys
```json
// Place your key bindings in this file to overwrite the defaults
[
  // Maximize current editor
  {
    "key": "cmd+k cmd+m",
    "command": "workbench.action.maximizeEditor",
    "when": "editorTextFocus"
  },
  // Exit Maximize current editor
  {
    "key": "cmd+k cmd+n",
    "command": "workbench.action.evenEditorWidths",
    "when": "editorTextFocus"
  }
]
```

## Packages
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
- TSLint
- Monokai theme
- VSCodeVim

## User Settings
```json
// Place your settings in this file to overwrite the default settings
{

    // The number of spaces a tab is equal to.
    "editor.tabSize": 2,
    "editor.renderIndentGuides": true,
    "files.trimTrailingWhitespace": true,

    "files.exclude": {
      "**/*.js": {"when": "$(basename).ts"},
      "**/*.js.map": true
    },

    "files.autoSave": "off",
    "editor.renderWhitespace": "boundary",
    "editor.lineNumbers": "on",
    
    
    // OPTIONAL
    // Configure glob patterns for excluding files and folders in searches. Inherits all glob patterns from the files.exclude setting.
  "search.exclude": {
    "**/node_modules": true,
    "**/bower_components": true,
    "**/build": true
  }
}
```

## Setup

#### How to add an "Open with VS Code" icon in Finder toolbar? 
![](/img/vscode-open-folder-from-toolbar.gif)
Go to my repo [open-folder-with-vs-code](https://github.com/hamxiaoz/open-folder-with-vs-code) and follow the instructions.
