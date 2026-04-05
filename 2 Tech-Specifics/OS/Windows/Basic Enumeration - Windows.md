---
tags:
  - "#type/tech-specific"
  - "#attack/collection"
  - "#attack/discovery"
---
# Fundamentals

See [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows|Fundamentals - Windows]].

During enumeration, never forget to cross-connect information to gather value. E.g. a running process that binds to port 443, that has an executable, configuration files, a specific software version, etc.

**Tools:**

- [[3 Tools/shells/cmd|cmd]]
- [[3 Tools/shells/PowerShell|PowerShell]]

**Hint:** PowerShell can run all commands available on the system, including cmd.

# Pentesting

**Workflow:**

1. Get an overview of the current system
2. Perform in-depth enumeration - also see [[2 Tech-Specifics/OS/Windows/Privilege Escalation - Windows/Privilege Escalation Vectors - Windows|Privilege Escalation Vectors - Windows]]

## Enumerate Users, Groups & Domain

- infer further purpose, characteristics & possible privileges of the user
- e.g. help desk staff, admins, developers, accounting,...

| Purpose                             | Command                                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------------------- |
| list users                          | cmd: `net user`<br>PowerShell: `Get-LocalUser`                                               |
| list details & privileges of a user | `net user <username>`                                                                        |
| show current users privileges       | `whoami /priv`                                                                               |
| list groups of the current user     | `whoami /groups`                                                                             |
| list other logged in users          | `qwinsta`                                                                                    |
| show local groups                   | cmd: `net localgroup`<br>PowerShell: `Get-LocalGroup` (also shows group descriptions)        |
| list members of group               | cmd: `net localgroup <groupname>`<br>PowerShell: `Get-LocalGroupMember <groupname>`          |
| show domain                         | PowerShell: `powershell (Get-CimInstance Win32_ComputerSystem).Domain` and `$env:USERDOMAIN` |
| list cached kerberos tickets        | `klist`                                                                                      |

### Relevant Built-In Groups

- Administrators: Local Administrators of the machine
- Backup Operators: can read & write also files the don't own
- Remote Desktop Users: can log in via [[2 Tech-Specifics/Network/Protocols/RDP|RDP]]
- Remote Management Users: can log via [WinRM](https://learn.microsoft.com/en-us/windows/win32/winrm/portal)

## System Information

| Purpose                                                                                                                                                                 | Command                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| show detailed system info<br>Based on the build number, derive the windows version using [Wikipedia](https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions). | cmd: `systeminfo`<br>PowerShell: `Get-ComputerInfo`                                                                                                                                                                                       |
| show windows version                                                                                                                                                    | cmd: `ver`                                                                                                                                                                                                                                |
| show the hostname - might indicate its purpose                                                                                                                          | `hostname`                                                                                                                                                                                                                                |
| list running processes                                                                                                                                                  | PowerShell: `Get-Process`<br>cmd: `tasklist`                                                                                                                                                                                              |
| List installed security updates                                                                                                                                         | `Get-CimInstance -Class win32_quickfixengineering \| Where-Object { $_.Description -eq "Security Update" }`                                                                                                                               |
| List installed updates                                                                                                                                                  | `wmic qfe get Caption,Description,HotFixID,InstalledOn`                                                                                                                                                                                   |
| Get integrity level of current process                                                                                                                                  | use [[3 Tools/microsoft/Sysinternals#Process Explorer\|Process Explorer]]<br>use third party powershell modules: [NtObjectManager](https://www.powershellgallery.com/packages/NtObjectManager/1.1.33) --> `Get-NtTokenIntegrityLevel`<br> |

## Network

| Purpose                                          | Command                       |
| ------------------------------------------------ | ----------------------------- |
| list all network interfaces                      | `ipconfig /all`               |
| display routing table                            | `route print`                 |
| list active network connections and related PIDs | `netstat -ano`                |
| get process name of specified PID                | `tasklist /FI "PID eq <PID>"` |

**Relevant information:**

- Are IPs set manually --> might be a server
- routing table might reveal other systems or network segments without creating noise
- Type and PID of services bound to network interface --> match services with [[#Installed Applications]]
- Services running only on localhost often have weaker security measures than external facing services.

## Antivirus Enum

2 options: search for antivirus explicitely or list all running services and checking for antivirus

| Purpose                                                   | Command                                                |
| --------------------------------------------------------- | ------------------------------------------------------ |
| search for "windefend" service                            | `sc query windefend`                                   |
| list all active services                                  | `sc queryex type=service`                              |
| view running services (filter with `findstr "[keyword]"`) | `wmic service get name,displayname,pathname,startmode` |

## File Searching

See [[3 Tools/shells/cmd|cmd]] and [[3 Tools/shells/PowerShell|PowerShell]].
