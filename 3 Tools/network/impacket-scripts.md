---
tags:
  - "#type/tool"
  - "#attack/lateral-movement"
  - "#attack/execution"
Link: https://www.kali.org/tools/impacket-scripts/
Purpose: python-based networking multitool
---
# Info

impacket is a python module that supports networking tasks

- makes working with network protocols in python easier
- supports both low level (IP, UDP, TCP) and high level (NMB, SMB) protocols
- Contains lots of modules for different protocols

**impacket-scripts** contains many for various purposes

# Impacket-mssqlclient

**Purpose:** connect to a [[2 Tech-Specifics/Database/MSSQL|MSSQL]] database.

**Usage:**`username:password@<address>`

Use NTLM auth instead of kerberos: `-windows-auth`

# Impacket-psexec

Emulates the behaviour of [[3 Tools/windows/Sysinternals#PsExec|PsExec]].

**Purpose:** [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash|Pass the Hash]] - (provides a shell with **SYSTEM** privileges.)

**Usage:** `impacket-psexec -hashes <LM_hash>:<NTLM_hash> <user>@<IP>`

**Note:** If no LM hash is available, fill it with 32 zeros: `00000000000000000000000000000000`

# Impacket-wmiexec

Uses [Windows Management Instrumentation (WMI)](https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page) to execute commands on a remote system.

**Purpose:** [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash|Pass the Hash]]

**Example Usage:** `impacket-psexec -hashes <LM_hash>:<NTLM_hash> <user>@<IP>`

**Note:** If no LM hash is available, fill it with 32 zeros.

# Impacket-ntlmrelayx

Relays NTLM authentication to another machine.

**Purpose:** [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#NTLMv2 Relay Attack|NTLMv2 Relay Attack]]

**Example Usage:** `impacket-ntlmrelayx --no-http-server -smb2support -t <target-ip> -c "<command_to_execute>"`
