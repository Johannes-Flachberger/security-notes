---
tags:
  - "#type/tool"
Link: https://tartarus.org/~simon/putty-snapshots/htmldoc/Chapter7.html
Purpose: ssh client for windows
---
# Info

Plink is "the" command line alternative for putty, before [[3 Tools/shells/ssh|ssh]] was included in windows.

Supports most of openssh features, except Remote Dynamic Port Forwarding.

On kali available at `/usr/share/windows-resources`.

# Usage

`plink.exe -ssh -l <user> -pw <password> <ip>`

See [[3 Tools/shells/ssh|ssh]] for port forwarding options.

# Snippets
