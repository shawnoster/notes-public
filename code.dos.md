---
id: GNHxIwUuojNODtHKJu9Au
title: DOS Command-Line
desc: ''
updated: 1654975380262
created: 1634939498231
---

# Command-Line/DOS

### Using Aliases to Save Key Strokes

If you can't be bothered to untrain the muscle memory of using the command line instead of PowerShell or bash then at least make your life a little easier by setting up some aliases for often typed commands. These are mine:

```bash
@echo off

DOSKEY ls=dir
DOSKEY tam=python c:\tam\tam.py $*
DOSKEY pp=python -m json.tool $*
```

_Fun Fact_ The `$*` denotes that everything after the aliaes should be passed through.

### Load them every time

1. Create a bat or cmd file
2. Put all your doskey tricks in it
3. Create a shortcut for c:\windows\system32\cmd.exe
4. In the shortcut's properties change it to `c:\windows\system32\cmd.exe  /K "C:\Users\Shawn\Dropbox (Personal)\Tools\doskey-aliases.cmd"`
5. Change **Start In** to `%HOMEDRIVE%%HOMEPATH%`
6. Save, Run
