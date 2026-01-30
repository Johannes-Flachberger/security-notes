---
tags:
  - "#type/tech-specific"
  - "#attack/lateral-movement"
  - "#attack/initial-access/client-side"
  - "#attack/initial-access/server-side"
---
# Fundamentals

See [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page)

Uses [[2 Tech-Specifics/Network/Protocols/TCP 135 msrpc|TCP 135 msrpc]] to create a session and the performs [RPCs](https://learn.microsoft.com/en-us/windows/win32/rpc/rpc-start-page) to perform tasks on a remote machine.

# Pentesting

## Initial Access & Lateral Movement

Using valid credentials, or pass-the-hash, WMI can be used for remote access.

**Prerequisites:**

- Port 135 (RPC Endpoint Mapper)
- Port 445 (SMB) - for the underlying DCOM transport
- Dynamic RPC ports (often 49152-65535)
- local "Administrator" user or Domain user with local admin rights on server
- WMI service running on the target

**Tools:**
- [[3 Tools/network/impacket-scripts#Impacket-wmiexec|impacket-wmiexec]]
- [[3 Tools/shells/cmd|cmd]]: historically `wmic` was used, but its deprecated
- [[3 Tools/shells/PowerShell#WMI command execution|PowerShell]]

# Hardening
