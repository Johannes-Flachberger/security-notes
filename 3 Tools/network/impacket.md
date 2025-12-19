---
tags:
  - "#type/tool"
Link: https://www.kali.org/tools/impacket/
Purpose: make working with network protocols in python easier
---
# Info
- makes working with network protocols in python easier
- supports both low level (IP, UDP, TCP) and high level (NMB, SMB) protocols
- Contains lots of modules for different protocols
# Usage

# Snippets
#### impacket-mssqlclient
To connect to a [[2 Tech-Specifics/Database/MSSQL|MSSQL]] database:
`username:password@<address>`
Use NTLM auth instead of kerberos:  `-windows-auth`