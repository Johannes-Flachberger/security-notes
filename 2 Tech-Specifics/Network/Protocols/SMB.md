---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
  - "#attack/exfiltration"
  - "#attack/initial-access/server-side"
---
# Fundamentals

SMB - Server Message Block

**Default Ports:** tcp445

Purpose: remote access to files and printers

SMB often goes along with [[2 Tech-Specifics/Network/Protocols/netbios|netbios]], which was historically used by windows

**SMB Workgroup**

identifies a group of machines that have access to each others smb shares

**SMB Share**

a folder or printer that is shared

access right can be set for each share

# Pentesting

**Workflow:**

1. get credentials - see [[#Password Attacks]]
2. Enumerate Workgroup, Shares, Permissions,... - see [[#Enumeration]]
3. Access files - see [[#Exfiltration]] and [[#SMB Commands Cheat Sheet]]

## Password Attacks

Legacy systems or misconfigured systems might support "guest access" without authentication. Try:

- Usernames `Guest`, `ANONYMOUS LOGON`, `nobody`
- Null Session: empty user and password

Also see [[1 Methods/Security-Testing/8 Credential Access/Overview - 8 Credential Access|Credential Access]], or try a [[1 Methods/Security-Testing/3 Initial Access/Password Attacks|Dictionary Attack]].

**Tools:**

- [[3 Tools/bruteforce/netexec|netexec]]: password spraying (very good for windows/AD environments)
- [[3 Tools/bruteforce/Hydra|Hydra]]

## Enumeration

This does not cover enumeration of files within an smb share - for that see [[#Exfiltration]]

> [!NOTE] Note
> In-depth SMB enumeration requires valid credentials, unless guest logon is allowed. --> first get [[1 Methods/Security-Testing/8 Credential Access/Overview - 8 Credential Access|Credential Access]]

**Tools:**

- [[3 Tools/network/scanning/nmap snippets#SMB Enumeration|nmap]]: vulnerability scanning (use `nmap --script smb-vuln-*`)
- [[3 Tools/bruteforce/netexec|netexec]]: password spraying, version enumeration, OS detection, share listing
- [[3 Tools/network/smb/smbclient|smbclient]]: manual smb connection
- [[3 Tools/network/net (windows built-in)|net (windows built-in)]]: use from windows
- RPC enumeration:
	- [enum4linux-ng](https://www.kali.org/tools/enum4linux-ng/): automated user/group/policy enumeration
	- `rpcclient`: manual rpc enumeration (users/groups/policies)

**Deprecated Tools:**

- nbtscan
- enum4linux

## Exfiltration

Search through and browse data on smb shares.

**Tools:**

- [[3 Tools/network/smb/smbmap|smbmap]]: recursive directory listing, remote file searching
- [[3 Tools/network/smb/Smbget|Smbget]]: recursive download of whole shares
- [[3 Tools/network/smb/smbclient|smbclient]]: manual smb connection
- [[3 Tools/network/net (windows built-in)|net (windows built-in)]]: use from windows

## Execution

**Tools:**

- [[3 Tools/network/impacket-scripts#Impacket-wmiexec|impacket-wmiexec]]: uses WMI over SMB, similar to psexec but stealthier, no service creation
- [[3 Tools/network/impacket-scripts#Impacket-psexec|impacket-psexec]]: see [[#PsExec]]
- `impacket-smbexec`: similar to psexec but stealthier (no binary creation)
- [[3 Tools/exploitation frameworks/Metasploit/Overview - Metasploit|Metasploit]]: `exploit/windows/smb/psexec`

### PsExec

**Prerequisites:**

- Windows target
- username of localadmin on the target
- NTLM hash or password of the target user
Use, or emulate the behaviour of [[3 Tools/microsoft/Sysinternals#PsExec|Psexec]], a tool to execute commands on remote machines using [[2 Tech-Specifics/Network/Protocols/SMB|SMB]].

## SMB Commands Cheat Sheet

| Command          | Purpose                        |
| ---------------- | ------------------------------ |
| `ls`             | List files and directories     |
| `cd <dir>`       | Change remote directory        |
| `pwd`            | Show current remote directory  |
| `lcd <dir>`      | Change local working directory |
| `get <file>`     | Download a single file         |
| `get <file> - `  | print file contents            |
| `put <file>`     | Upload a single file           |
| `mget <pattern>` | Download multiple files        |
| `mput <pattern>` | Upload multiple files          |
| `rm <file>`      | Delete a remote file           |
| `mkdir <dir>`    | Create a remote directory      |
| `rmdir <dir>`    | Remove a remote directory      |
| `print <file>`   | Send a file to a printer share |
| `exit`           | Close the connection           |
