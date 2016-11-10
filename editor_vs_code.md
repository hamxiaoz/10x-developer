# Editor: VS Code

## Hotkeys

Navigation
- Toggle side pane: `CMD+B`
- Switch to file pane: `SHIFT+CMD+E` (How to remember? Same hotkey prefix for find: `SHIFT+CMD+F`)
- Switch to focus group 1/2: `CMD+1/2`
- open in new pane: `CMD+\`

**Advanced**
- navigate back to last position/file: `CTRL+-`
- find by symbol (instead of find by text): `CMD+SHIFT+o`

Search:
- Switch search history: `ALT+UP/DOWN` 

Terminal: "ctrl+`"

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