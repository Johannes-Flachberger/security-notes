**Tags:** #type/tech-specific 

---
## python
1. `python -c 'import pty; pty.spawn("/bin/sh")'` or `python2 ...` or `python3 ...` - spawns bash shell using python
2. `export TERM=xterm` - gives access to terminal commands like "clear"
3. background shell wiht `ctrl + z´
4. `stty raw -echo; fg` - deactivate echo of own terminal, you can reactivate it with `reset`