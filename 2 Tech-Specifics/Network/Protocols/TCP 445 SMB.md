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
2. Enumerate Workgroup, Shares, Permissions,...
3. Access files - see [[#Exfiltration]]

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
