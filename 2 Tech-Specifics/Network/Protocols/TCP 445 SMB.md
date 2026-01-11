---
tags:
  - "#type/tech-specific" 
  - "#attack/reconnaissance/active" 
  - "#attack/exfiltration" 
---
# Fundamentals

default port: 445

Purpose: remote access to files and printers

SMB often goes along with [[2 Tech-Specifics/Network/Protocols/TCP 139 netbios|netbios]], which was historically used by windows

**SMB Workgroup**
identifies a group of machines that have access to each others smb shares
**SMB Share**
a folder or printer that is shared
access right can be set for each share

# Pentesting

## Workflow

1. get credentials - see [[#Credential Access]]
2. Enumerate Workgroup, Shares, Permissions,... - see [[#Enumeration]]
3. Access files - see [[#Exfiltration]] and [[#SMB Commands Cheat Sheet]]

## Credential Access

Legacy systems or misconfigured systems might support "guest access" without authentication. Try:

- Usernames `Guest`, `ANONYMOUS LOGON`, `nobody`
- Null Session: empty user and password

Also see [[1 Methods/Security-Testing/8 Credential Access/Overview - 8 Credential Access|Credential Access]], or try a [[1 Methods/Security-Testing/8 Credential Access/Bruteforce and Dictionary Attacks|Dictionary Attack]].

## Enumeration

> [!NOTE] Note
> SMB enumeration requires valid credentials. --> first get [[1 Methods/Security-Testing/8 Credential Access/Overview - 8 Credential Access|Credential Access]]

Tools:

- [[3 Tools/network/scanning/nmap snippets#SMB Enumeration|nmap]]
- [[3 Tools/network/SMB tools#Enumeration|SMB tools]]
- [[3 Tools/network/smbclient|smbclient]]
- [[3 Tools/network/impacket-scripts|impacket-scripts]]

## Exfiltration

Browse data on smb shares.

Tools:

- [[3 Tools/network/SMB tools#Exfiltration|SMB tools]]
- [[3 Tools/network/smbclient|smbclient]]
- [[3 Tools/shells/cmd|cmd]]

## Execution

### PsExec

**Prerequisites:**
- Windows target
- Admin username and NTLM hash or password available
Use, or emulate the behaviour of [PsExeec](https://learn.microsoft.com/en-us/sysinternals/downloads/psexec) - a [windows sysinternals tool](https://learn.microsoft.com/en-us/sysinternals/) to execute commands on remote machines using [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|SMB]].

**Tools:**
- [[3 Tools/network/impacket-scripts#Impacket-psexec|impacket-psexec]]
- [[3 Tools/exploitation frameworks/Metasploit/Overview - Metasploit|Metasploit]]: `exploit/windows/smb/psexec`

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
