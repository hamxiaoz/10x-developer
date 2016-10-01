# Development Setup/Tools

## Universal
- Pixlr, Photoshop online: https://pixlr.com/
- Sublime, see [this note](vim and st.md)

### Chrome Extension
- https://chrome.google.com/webstore/detail/builtwith-technology-prof/dapjbgnjinbpoindlpdmhochffioedbn
- https://chrome.google.com/webstore/detail/merge-windows/adjadgadeebehakpgamlnafmdkegkmph
- https://chrome.google.com/webstore/detail/web-developer-checklist/iahamcpedabephpcgkeikbclmaljebjp
- http://chrispederick.com/work/web-developer/
- http://chengyinliu.com/whatfont.html
- https://chrome.google.com/webstore/detail/emmet-review/epejoicbhllgiimigokgjdoijnpaphdp
- https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall
- postman: https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo
- https://chrome.google.com/webstore/detail/dimensions/baocaagndhipibgklemoalmkljaimfdj
- feedly, evernote

---



---

## Windows Development Tools

### Shell
- Shell/Console
    - ConEmu: https://conemu.github.io/
    - [Gow - The lightweight alternative to Cygwin](https://github.com/bmatzelle/gow)
    - [Clink](https://github.com/mridgers/clink) - windows shell enhancements

### Editor
- vim
- Sublime
- Atom

### VS Extension
- AnkhSVN, svn in Visual Stuio: https://ankhsvn.open.collab.net/
- Productivity Power Tools: https://visualstudiogallery.msdn.microsoft.com/d0d33361-18e2-46c0-8ff2-4adea1e34fef/
- ViEmu, bring vim mode home: http://www.viemu.com/
- ReSharper, write C# code more happy: https://www.jetbrains.com/resharper/
- TestDriven.net, unit tests: http://www.testdriven.net/ 

### Build
- Inno Setup, installer builder. Much better than the default windows one: http://www.jrsoftware.org/isinfo.php
- Inno Script Studio, GUI for inno: https://www.kymoto.org/products/inno-script-studio
- Albacore, task runner so you can do one click build: http://albacorebuild.net/
  - It requires ruby: http://rubyinstaller.org/
  - Install ruby add-on DevKit too: http://rubyinstaller.org/add-ons/devkit/
- Use batch file to call rake tasks so you can do **one click** build. See [bat examples](https://github.com/hamxiaoz/my-scripts)
  
    ```bat
    @ECHO OFF

    REM call rake
    call rake target=internal

    PAUSE
    ```


### Network
- WinSCP: https://winscp.net/eng/download.php
  - NOTE if you use WinSCP to transfter the script to the server, be sure to use "text" transfer settins, otherwise the script might contain dos CRLF line endings, see http://stackoverflow.com/questions/2920416/configure-bin-shm-bad-interpreter
- SuperPuTTY: https://github.com/jimradford/superputty

### Tools
- Paint.net, best photo editing tool on Windows: http://www.getpaint.net/index.html
- LICEcap, make .gif, it's also available on Mac: http://www.cockos.com/licecap/
- TotalCommander, 10x better than file explorer: http://www.ghisler.com/
- AHK, add global hotkey: https://autohotkey.com/

### VM
- FREE VM machines (all platform) from [Microsoft](https://dev.windows.com/en-us/microsoft-edge/tools/vms/windows/)
- Virtual Box: https://www.virtualbox.org/wiki/Downloads
- VMWare (commercial)

### More
Find more tools from 
- [Scott Hanselman's 2014 Ultimate Developer and Power Users Tool List for Windows](http://www.hanselman.com/blog/ScottHanselmans2014UltimateDeveloperAndPowerUsersToolListForWindows.aspx)
- https://github.com/RiseLedger/awesome-windows
