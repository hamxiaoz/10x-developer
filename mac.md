# Mac

## Hotkeys

- Jump to word: `ALT+arrow`
- Zoom in quick look: hold down `ALT/Option` (it seems you can zoom by guesture on El Capitan)
- ALT+SPACE to launch spotlight in spotlight settings
- screen capture:
  - 全屏截图 command + shift + 3；
  - 自由截图 command + shift + 4；
  - 窗口截图 command + shift + 4 =>空格健=>鼠标左键
- Paste without format: CMD+SHIFT+V
- 切换一个应用的不同窗口是 Command + \`
- 需要多次切换的程序可按住cnd+tab不放手，然后使用触摸板点击。

Less common:
- cmd + up 上一级文件夹（win里的退格键）
- cmd + down 打开当前选中的文件/夹（win里的回车）
- How to Access Menu like "ALT" in windows? Ctrl+F2, then you can type and hit enter.


## OS Settings

Finder:
- Edit toolbar to have: new folder, delete, and info
- Show file path at the bottom of finder window: 'View -> Show Path bar'
- show hidden files
    1. `defaults write com.apple.finder AppleShowAllFiles YES`
    3. Restart finder: hold the ‘Option/alt’ key, then right click on the Finder icon in the dock and click Relaunch.
- Copy path service: http://osxdaily.com/2013/06/19/copy-file-folder-path-mac-os-x/
- Open current folder in terminal: iterm2 has it or customize it from 'System Preferences > Keyboard > Keyboard Shortcuts > Services'. Look for "New Terminal at Folder" and "New Terminal Tab at Folder". You can also assign them shortcut keys.'
- Quick look plugin https://github.com/whomwah/qlstephen
- [open with VSCode](https://github.com/hamxiaoz/open-folder-with-vs-code)
- [open with sublime](https://github.com/hamxiaoz/open-folder-with-sublime)


System Preferences:
- Enable touchpad tap to click:`System Preferences > Trackpad，Point & Click: check Tap to click`
- Spotlight shortcut: OPTION+SPACE (so that I can use CMD+SPACE for IME)
- [How to enable keyboard access for "Don't save" on Mac?](http://zurassic.com/blog/TIL-how-to-enable-keyboard-access-for-donot-save-mac.html) "Enable `System Preferences > Keyboard -> Shortcuts: check All controls` then you can use `SPACE` to choose file dialog..."


## Tools

Essential:
- Chrome
- Chrome Canary
- VSCode
    - extension: vim, Prettier, GitLens
    - settings
    - install shell so we can do `code .`
- VSCode insider
- MacVim

Dev:
- git: `git --version`
- [ssh setup](https://help.github.com/en/articles/connecting-to-github-with-ssh)
- nvm
- brew
- `brew install tree`
- iTerm
- zsh
- terminal profile

Cloud:
- dropbox

System Tools
- [Spectacle: window management](https://www.spectacleapp.com/)
- [Keyboard remap: Karabiner-Elements](https://pqrs.org/osx/karabiner/)
  - crate new profile: 'HHKB'
  - remap the build-in keyboard:
    - backslash \ -> delete_or_backspace
    - caps_lock -> left_control
    - delete_or_backspace -> backslash \

DB GUI
  - MongoDB: [RoboMongo](https://robomongo.org/download)
  - MySQL: [Sequel Pro](https://www.sequelpro.com/)

Design Tools:
- Sketch
- Xmind(?)

Optional:
- Network: inject data to web: http://www.charlesproxy.com/
- VM: https://github.com/xdissent/ievms/
