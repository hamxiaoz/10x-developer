# Windows Development

## Essential Tools for Developer on Windows

### Shell
- Shell/Console
    - ConEmu2
    - [Gow - The lightweight alternative to Cygwin](https://github.com/bmatzelle/gow)
    - [Clink](https://github.com/mridgers/clink)

### Editor
- vim
- Sublime
- Atom

### VS Extension
..

### Build
- Inno Setup, installer builder. Much better than the default windows one: http://www.jrsoftware.org/isinfo.php
- Inno Script Studio, GUI for inno: https://www.kymoto.org/products/inno-script-studio
- Albacore, task runner so you can do one click build: http://albacorebuild.net/
  - It requires ruby: http://rubyinstaller.org/
  - Install ruby add-on DevKit too: http://rubyinstaller.org/add-ons/devkit/
- Use batch file to call rake tasks so you can do **one click** build.
  
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

### VM
- FREE VM machines (all platform) from [Microsoft](https://dev.windows.com/en-us/microsoft-edge/tools/vms/windows/)
- Virtual Box: https://www.virtualbox.org/wiki/Downloads
- VMWare (commercial)

Find more tools from [Scott Hanselman's 2014 Ultimate Developer and Power Users Tool List for Windows](http://www.hanselman.com/blog/ScottHanselmans2014UltimateDeveloperAndPowerUsersToolListForWindows.aspx)
