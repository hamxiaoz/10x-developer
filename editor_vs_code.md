# Editor: VS Code

- [ ] Migrate my Atom theme

Misc links:

- Custom snippets: https://code.visualstudio.com/docs/customization/userdefinedsnippets
- HTML with Emmet: http://code.visualstudio.com/docs/languages/html#_emmet-snippets

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
- Find by symbol (instead of find by text): `CMD+SHIFT+O`
  - When viewing JSON file, it'll find by the key.
  - When viewing HTML, it'll find by class or id.
- File navigation:
  - :punch: Show list of files in one editor or go back and forth between files: `CTRL+TAB`
  - `CTRL+-` to go back last file
  - to last position: `CMD+U`
- Code reformatting: `CMD+K, CMD+F`
- Code folding: `SHIFT+CMD+[ or ]`
- Trim trailing whitespace: `CMD+SHIFT+X`

Multi-cursor:

- In Insert mode, use `ALT/OPTION` + click to add multiple cursor, then press `ESC` to go to view mode.
- In Normal mode, use `CMD+D` to select multiple instances, then press `ESC` to go to view mode.
- In Insert mode, select lines and use `SHIFT+CMD+L` to turn lines into selections. (Require custom keyboard setup, see eblow)
- How to select all in file search result? `CMD+F` -> type search word -> `ALT + ENTER`
  ![](https://cloud.githubusercontent.com/assets/5047891/20052065/6b5c84b8-a4d2-11e6-8575-d506ebac3fe9.gif)

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
  },
  // Similar to Sublime, convert selection into line selections
  {
    "key": "cmd+shift+l",
    "command": "editor.action.insertCursorAtEndOfEachLineSelected",
    "when": "editorTextFocus"
  }

  // quick switch window: CMD+R
  {
    "key": "cmd+r",
    "command": "workbench.action.quickSwitchWindow"
  },
  {
      "key": "cmd+r",
      "command": "workbench.action.quickOpenNavigateNext",
      "when": "inWindowsPicker"
  }

  // focus on terminal
  {
    "key": "cmd+4",
    "command": "workbench.action.terminal.focus",
    "when": "!terminalFocus"
  },

]
```

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
            "args": [
                "-9",
                "grunt"
            ],
            "isShellCommand": true,
            "suppressTaskName": true,
            "showOutput": "never"
        },
        {
            "taskName": "lint",
            "command": "grunt",
            "args": [
                "lint"
            ],
            "isShellCommand": true,
            "suppressTaskName": true,
            "showOutput": "silent"
        }
    ]
}
```

## Debug

- You can press `F5` to debug any single file.
- Link to [doc](https://code.visualstudio.com/docs/editor/debugging)

## Packages

- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
- Monokai theme
- Diff Tool
- TSLint
- TSLint
- GitLens
- Markdown All in One
- Prettier
- Quokka.js
- SASS Formatter
- TypeScrip[t Import Sorter]
- Vim


- Prettify JSON
- Open Spec File

## Code Formatting Setup

https://medium.com/@hamxiaoz/visual-studio-code-formatting-setup-9f40a95699ce

## User Settings

```json
// Place your settings in this file to overwrite the default settings
{
  // core
  "editor.tabSize": 2,
  "editor.renderIndentGuides": true,
  "editor.cursorStyle": "line",
  "editor.cursorBlinking": "solid",
  "files.trimTrailingWhitespace": true,
  "editor.renderWhitespace": "boundary",
  "editor.lineNumbers": "on",
  "editor.minimap.enabled": false,
  "files.autoSave": "off",
  "editor.renderLineHighlight": "all",
  "workbench.colorCustomizations": {
    "editorIndentGuide.activeBackground": "#cba680c9"
  },
  "workbench.colorTheme": "Monokai Dimmed",
  "workbench.iconTheme": "vs-seti",
  "window.title": "${activeEditorLong}${separator}${rootName}",

  // vim
  "vim.disableAnnoyingNeovimMessage": true,
  "vim.disableExtension": false,
  "vim.easymotion": true,
  "vim.sneak": true,
  "vim.incsearch": true,
  "vim.useCtrlKeys": true,
  "vim.hlsearch": true,
  "vim.insertModeKeyBindings": [
      {
          "before": ["j","j"],
          "after": ["<Esc>"]
      }
  ],


  // OPTIONAL
  // Configure glob patterns for excluding files and folders in searches. Inherits all glob patterns from the files.exclude setting.
  "search.exclude": {
    "**/node_modules": true,
    "**/bower_components": true,
    "**/build": true
  },
  // Configure glob patterns for excluding files and folders.
  "files.exclude": {
    "**/*.js": { "when": "$(basename).ts" },
    "**/*.js.map": true,
    "**/.git": true,
    "**/.svn": true,
    "**/.hg": true,
    "**/.DS_Store": true,
    "**/.meteor": true
  },


  // HTML (default support by VS Code)
  // https://code.visualstudio.com/docs/languages/html#_formatting
  "html.format.wrapAttributes": "force-aligned",
  "html.format.enable": true,

  // SASS Formatter
  "sassFormat.indent": 2,
  "sassFormat.useSingleQuotes": true,

  // Prettier
  "prettier.singleQuote": true,
  "prettier.printWidth": 140, // or 120, for *.ts file we change width to 180

  // markdown
  "markdown.preview.breaks": true,
  // Set the style file name. for example: github.css, monokai.css ... https://github.com/isagalaev/highlight.js/tree/master/src/styles
  "markdown-pdf.highlightStyle": "monokai.css",
  // A list of URLs or local paths to CSS style sheets to use from the markdown preview. Relative paths are interpreted relative to the folder open in the explorer. If there is no open folder, they are interpreted relative to the location of the markdown file. All '\' need to be written as '\\'.
  "markdown.styles": [
    "https://raw.githubusercontent.com/isagalaev/highlight.js/master/src/styles/monokai.css"
  ],

  // codelens
  "typescript.referencesCodeLens.enabled": false,
  "git.enableSmartCommit": true,
  "gitlens.codeLens.enabled": true,
  "gitlens.advanced.messages": {
    "suppressCommitHasNoPreviousCommitWarning": false,
    "suppressCommitNotFoundWarning": false,
    "suppressFileNotUnderSourceControlWarning": false,
    "suppressGitVersionWarning": false,
    "suppressLineUncommittedWarning": false,
    "suppressNoRepositoryWarning": false,
    "suppressResultsExplorerNotice": true,
    "suppressShowKeyBindingsNotice": true
  },
  "gitlens.keymap": "none",
  "gitlens.historyExplorer.enabled": true,

  // Extension: Open Spec File
  "openSpecFile.suffixMap": {
    ".ts": ".spec.ts",
    ".js": ".spec.js",
  },

  // TypeScript Import Sorter
  // Left number of spaces for the new lined imports
  "importSorter.importStringConfiguration.tabSize": 2,
  // The count of units before import is newlined
  "importSorter.importStringConfiguration.maximumNumberOfImportExpressionsPerLine.count": 140,
  // The default order level of everything which is not include into rules
  "importSorter.sortConfiguration.customOrderingRules.rules": [
    {
      "regex": "^@angular",
      "orderLevel": 0,
      "numberOfEmptyLinesAfterGroup": 0
    },
    {
      "regex": "^[@]",
      "orderLevel": 10
    },
    {
      "regex": "^[a-zA-Z]", // 'rxjs/'
      "orderLevel": 10
    },
    {
      "regex": "^[.]",
      "orderLevel": 30
    }
  ],
}
```

## Setup

#### How to add an "Open with VS Code" icon in Finder toolbar?

![](/img/vscode-open-folder-from-toolbar.gif)
Go to my repo [open-folder-with-vs-code](https://github.com/hamxiaoz/open-folder-with-vs-code) and follow the instructions.
