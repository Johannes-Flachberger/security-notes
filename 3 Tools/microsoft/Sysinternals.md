---
tags:
  - "#type/tool"
Link: https://learn.microsoft.com/en-us/sysinternals/
Purpose: windows system utilities
---
# Info

A suite of windows systemadmin utilities, that can be used for various purposes

# PsExec

**Purpose:** execute commands on remote machines using SMB. Further information: [[2 Tech-Specifics/Network/Protocols/SMB#PsExec|SMB]]

**Prerequitsites:**
1. the authentication user must be in the local "Administrators" group on the target
2. the target must have an [[2 Tech-Specifics/Network/Protocols/SMB|SMB]] service enabled (default on Windows Server)
3. the `ADMIN$`smb share must be available (default on Windows Server)

**Usage:**

User & Password Authentication: `.\PsExec64.exe -i  \\<hostname/ip> -u <domain>\<user> -p <password> <command_to_execute>`

Kerberos Authentication (assumes that a TGT is already cached): `PsExec64.exe \\ <hostname/ip> <command_to_execute>`

e.g. use `cmd` or `powershell` as command to spawn a shell

Alternative Tools:

- [[3 Tools/network/impacket-scripts#Impacket-psexec|impacket-psexec]]
- [[3 Tools/exploitation frameworks/Metasploit/Overview - Metasploit|Metasploit]]: `exploit/windows/smb/psexec`

# Process Explorer

**Purpose:** Get detailed info about running processes.

# ProcMon

**Purpose:** detailed analysis of a running process / executable. Useful to list the used DLLs.

**List DLLs:**

Since it requires admin privileges, mirror the target setup for preparation. ProcMon can be overwhelming. Filter for the target process name, the DLL name, take actions & relate the events to the actions.

# PsLoggedOn

**Purpose:** List logged on users.

**Prerequisite:** Remote Registry Service must be enabled
- disabled per default since Windows 8
- enabled per default on Windows Server

**Usage:** `.\PsLoggedon.exe \\<hostname>`

Snippet to check multiple hosts at once, e.g. resulting from Powerview:

```powershell
Foreach($host in $computers)
{
     $comp.cn
     .\PsLoggedon.exe "\\$($host.cn)"
     Write-Host "---------------------------------------------------"
 }
```

Might also list the user issuing the PsLoggedOn command, since it needs to create a session to work.

Uses [NetSessionEnum](https://learn.microsoft.com/en-us/windows/win32/api/lmshare/nf-lmshare-netsessionenum).
