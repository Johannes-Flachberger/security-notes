---
tags:
  - "#type/tech-specific"
  - "#attack/lateral-movement"
  - "#attack/initial-access"
---
# Fundamentals

WinRM - Windows remote management

**Defaults Ports:**

- tcp5985
- tcp5986

basically [[2 Tech-Specifics/_Other/File Formats/XML|XML]] over [[2 Tech-Specifics/Network/Protocols/HTTP(S)|HTTP(S)]].

Used by default by [[3 Tools/shells/PowerShell#PowerShell Remoting|PowerShell Remoting]]

**Ressources:**

- [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/winrm/portal)

# Pentesting

## Initial Access & Lateral Movement

**Note:** Chaining a bind shell, such as most [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Remote Shells]] with a winrm connection does not work well.

**Prerequisites:**

- User that connects must be in one of the following groups:
- `Remote Management Users`
- `Administrators`

**Tools:**

- [evil-winrm](https://github.com/Hackplayers/evil-winrm):
	- Usage: `evil-winrm -i <ip> -u <user> -p "<password>"`
	- supports [[2 Tech-Specifics/OS/Windows/Lateral Movement - Windows/Pass the Hash|Pass the Hash]]
- [winrs](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/winrs): built in windows remote management utility
	- Because of [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#UAC|UAC]], this works only from domain users.
	- e.g. use a [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Reverse Shell]] as payload.
	- `winrs -r:<ip/hostname> -u:<user> -p:<password>  "<command>"`
- [[3 Tools/shells/PowerShell#PowerShell Remoting|PowerShell Remoting]]

# Hardening
