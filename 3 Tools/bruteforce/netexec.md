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

- [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|TCP 445 SMB]]
- [[3 Tools/shells/ssh|ssh]]
- [[2 Tech-Specifics/Network/Protocols/TCP,UDP 389 LDAP|TCP,UDP 389 LDAP]]
- [[2 Tech-Specifics/Network/Protocols/TCP 20,21 FTP|TCP 20,21 FTP]]
- wmi
- [[2 Tech-Specifics/Network/Protocols/TCP 5985,5986 WinRM|winrm]]
- [[2 Tech-Specifics/Network/Protocols/TCP 3389 RDP|TCP 3389 RDP]]
- vnc
- [[2 Tech-Specifics/Database/MSSQL|MSSQL]]
- [[2 Tech-Specifics/Network/Protocols/TCP 111,2049 NFS|TCP 111,2049 NFS]]

# Usage

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
