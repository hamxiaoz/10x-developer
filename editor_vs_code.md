# Editor: VS Code

## [Learning](http://code.visualstudio.com/docs)

**Advanced**
- navigate back:
  - to last file: `CTRL+-`
  - to last position: `CMD+U`
- find by symbol (instead of find by text): `CMD+SHIFT+o`
- Go to line: `:20`
- Code reformatting: `CMD+K, CMD+F`
- Code folding: `SHIFT+CMD+[ or ]`
- Trigger Intellisense: `CTRL+SPACE`
- Trim trailing whitespace: `CMD+SHIFT+X`

_ [Everything git](https://github.com/Microsoft/vscode-tips-and-tricks#task-runner)

_ custom snippets

_ [Emmet](http://code.visualstudio.com/docs/languages/html#_emmet-snippets)

_ Debug


## Hotkeys

Sidebar
- Toggle side pane: `CMD+B`
- Switch to file pane: `SHIFT+CMD+E` (How to remember? Same hotkey prefix for find: `SHIFT+CMD+F`)

Navigation in Editor
- Switch to focus group 1/2: `CMD+1/2`
- open in new pane: `CMD+\`
- Move active editor to left/right group: `CTRL+CMD+LEFT/RIGHT`
  ```
  { "key": "ctrl+cmd+right",        "command": "workbench.action.moveEditorToNextGroup" },
  { "key": "ctrl+cmd+left",         "command": "workbench.action.moveEditorToPreviousGroup" }
```



Search:
- Switch search history: `ALT+UP/DOWN` 

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