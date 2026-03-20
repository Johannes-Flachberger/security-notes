---
tags:
  - "#type/tool"
  - "#attack/credential-access"
  - "#attack/discovery"
Link: https://www.netexec.wiki/
Purpose: automated network security assessment tool for large networks
---
# Info

versatile & automated network security assessment tool

Check the wiki for features: https://www.netexec.wiki/

supports various popular protocols:

- [[2 Tech-Specifics/Network/Protocols/SMB|SMB]]
- [[3 Tools/shells/ssh|ssh]]
- [[2 Tech-Specifics/Network/Protocols/LDAP|LDAP]]
- [[2 Tech-Specifics/Network/Protocols/FTP|FTP]]
- [[2 Tech-Specifics/OS/Windows/WMI|WMI]]
- [[2 Tech-Specifics/Network/Protocols/WinRM|winrm]]
- [[2 Tech-Specifics/Network/Protocols/RDP|RDP]]
- vnc
- [[2 Tech-Specifics/Database/MSSQL|MSSQL]]
- [[2 Tech-Specifics/Network/Protocols/NFS|NFS]]

# Usage

The nxc wiki is pretty good: https://www.netexec.wiki/

Example: `nxc smb <ip> -u <user> -p '<password>' -d <domain> --continue-on-success`

- specify a range of IPs: e.g.`192.168.0.100-200`
- user/password files are also supported

Output:

- credentials are prepended with `[+]` if valid and `[-]` if invalid
- when a user is cracked, it also shows `(Pwn3d!)` beside the credentials if the user has local admin privileges.

**Caution:** nxc does not check or respect the windows account policy.

> [!Hint] nxc only checks if authentication is successful, but not if a user is granted access on the application layer
> E.g. If credentials show as valid for RDP, that does not automatically mean that the user is authorised to log in via RDP.

# Snippets
