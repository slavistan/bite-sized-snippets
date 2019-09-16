---
layout: what-ive-learned
title: Write output to console
tags: autohotkey
is_wil_snippet: true
---

**tl;dr** Pipe the output of `FileOpen("*", "w").WriteLine("Hello World!")` to the active terminal.
  
For some reason AutoHotkey is incapable of directly printing output the shell in which the script was run. To
circumvent this redirect the output into a file or the active terminal.

```ahk
; myscript.ahk

; Win+o prints debug message
#o::FileOpen("*", "w").WriteLine("Hello World")
```

Now run the script via `AutoHotkeyU64.exe myscript.ahk > $(tty) &`. `tty` returns the active terminal's identifier.
Additionally, the process needs to be run in the background or AutoHotkey won't find any stdout to print to.
