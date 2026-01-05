---
tags:
  - "#type/tech-specific"
---
# Fundamentals

Windows remote management tool

Alternatively, [[2 Tech-Specifics/Network/Protocols/TCP 22 SSH|SSH]] can be used for PowerShell remoting

**Ressources:**
- https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/08-powershell-remoting
- https://learn.microsoft.com/en-us/windows/win32/winrm/portal

**Requirements:**
- User that connects must be in the `Remote Management Users` group

# Pentesting

**Note:** Chaining a bind shell, such as most [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Remote Shells]] with a winrm connection does not work well.

**Tools:**
- [evil-winrm](https://github.com/Hackplayers/evil-winrm):
	- Usage: `evil-winrm -i <ip> -u <user> -p "<password>"`
	- supports [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows|Pass the hash]]

# Hardening
