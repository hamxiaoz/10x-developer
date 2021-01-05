# Mac

## Hotkeys

* Jump to word: `ALT+arrow`
* Zoom in quick look: hold down `ALT/Option` \(it seems you can zoom by guesture on El Capitan\)
* ALT+SPACE to launch spotlight in spotlight settings
* screen capture:
  * 全屏截图 command + shift + 3；
  * 自由截图 command + shift + 4；
  * 窗口截图 command + shift + 4 =&gt;空格健=&gt;鼠标左键
* Paste without format: CMD+SHIFT+V
* 切换一个应用的不同窗口是 Command + \`
* 需要多次切换的程序可按住cnd+tab不放手，然后使用触摸板点击。

Less common:

* cmd + up 上一级文件夹（win里的退格键）
* cmd + down 打开当前选中的文件/夹（win里的回车）
* How to Access Menu like "ALT" in windows? Ctrl+F2, then you can type and hit enter.

Mac support emac hotkey for moving cursors \([https://jblevins.org/log/kbd](https://jblevins.org/log/kbd)\):

* Control-F 光标前进一个字符，相当于右键（F = Forward）
* Control-B 光标后退一个字符，相当于左键（B = Backward）
* Control-P 上移一行，相当于上键（P = Previous）
* Control-N 下移一行，相当于下键（N = Next）
* Control-A 移动到一行的开头（A = Ahead）
  * Control-Shift-A 选中从光标开始，到一行开头的所有文字
* Control-E 移动到一行的结尾（E = End
  * Control-Shift-E 选中从光标开始，到一行结尾的所有文字
* Control-H 删除光标前面的字符
* Control-D 删除光标后面的字符
* Control-K 删除从光标开始，到一行结尾的所有字符

Chrome:

* history go back: `CMD + [`

Remap keys for HHKB:

* Remmap software: Karabiner-Element
* create layout: [http://www.keyboard-layout-editor.com/](http://www.keyboard-layout-editor.com/)
* use key map so Option 加 IKJL 等於 上下左右

## OS Settings

Finder:

* Edit toolbar to have: new folder, delete, and info
* Show file path at the bottom of finder window: 'View -&gt; Show Path bar'
* show hidden files
  1. `defaults write com.apple.finder AppleShowAllFiles YES`
  2. Restart finder: hold the ‘Option/alt’ key, then right click on the Finder icon in the dock and click Relaunch.
* Copy path service: [http://osxdaily.com/2013/06/19/copy-file-folder-path-mac-os-x/](http://osxdaily.com/2013/06/19/copy-file-folder-path-mac-os-x/)
* Open current folder in terminal: iterm2 has it or customize it from 'System Preferences &gt; Keyboard &gt; Keyboard Shortcuts &gt; Services'. Look for "New Terminal at Folder" and "New Terminal Tab at Folder". You can also assign them shortcut keys.'
* Quick look plugin [https://github.com/whomwah/qlstephen](https://github.com/whomwah/qlstephen)
* [open with VSCode](https://github.com/hamxiaoz/open-folder-with-vs-code)
* [open with sublime](https://github.com/hamxiaoz/open-folder-with-sublime)

System Preferences:

* Enable touchpad tap to click:`System Preferences > Trackpad，Point & Click: check Tap to click`
* Spotlight shortcut: OPTION+SPACE \(so that I can use CMD+SPACE for IME\)
* [How to enable keyboard access for "Don't save" on Mac?](http://zurassic.com/blog/TIL-how-to-enable-keyboard-access-for-donot-save-mac.html) "Enable `System Preferences > Keyboard -> Shortcuts: check All controls` then you can use `SPACE` to choose file dialog..."

## Tools

Essential:

* Chrome
* Chrome Canary / Firefox / Edge
* VS Code
  * extensions are sync via Github, turn on sync in vs code
  * install command line tool so we can do `code .`
* VSCode insider
* MacVim

Dev:

* iTerm and import profile from my dot files repo
* oh my zsh and import zshrc from my dot files repo
* brew and `brew install tree`
* git: `git --version` then `git config --global --edit`
* [ssh setup](https://help.github.com/en/articles/connecting-to-github-with-ssh)
* nvm and `nvm install --lts` (install lts version)


Cloud:

* dropbox

System Tools

* Windows management tool: [Rectangle](https://github.com/rxhanson/Rectangle) `brew install --cask rectangle`
* [Keyboard remap: Karabiner-Elements](https://pqrs.org/osx/karabiner/)
  * crate new profile: 'HHKB'
  * remap the build-in keyboard:
    * backslash  -&gt; delete\_or\_backspace
    * caps\_lock -&gt; left\_control
    * delete\_or\_backspace -&gt; backslash \

DB GUI

* MongoDB: [RoboMongo](https://robomongo.org/download)
* MySQL: [Sequel Pro](https://www.sequelpro.com/)

Design Tools:

* Figma (or Sketch)
* LucidChart (or Xmind)

Optional:

* Network: inject data to web: [http://www.charlesproxy.com/](http://www.charlesproxy.com/)
* VM: [https://github.com/xdissent/ievms/](https://github.com/xdissent/ievms/)

