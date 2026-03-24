---
tags:
  - "#type/tech-specific"
  - "#attack/collection"
  - "#attack/discovery"
---
# Fundamentals

See:

- [[3 Tools/shells/cmd|cmd]]
- [[3 Tools/shells/PowerShell|PowerShell]]

**Hint:** PowerShell can run all commands available on the system, including cmd.

# Pentesting

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

- Administrators:
- Backup Operators: can read & write also files the don't own
- Remote Desktop Users: can log in via [[2 Tech-Specifics/Network/Protocols/RDP|RDP]]
- Remote Management Users: can log via [WinRM](https://learn.microsoft.com/en-us/windows/win32/winrm/portal)

## System Information

| Purpose                                                                                                                                                                 | Command                                                                                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| show detailed system info<br>Based on the build number, derive the windows version using [Wikipedia](https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions). | cmd: `systeminfo`<br>PowerShell: `Get-ComputerInfo`                                                                                                                                                                                     |
| show windows version                                                                                                                                                    | cmd: `ver`                                                                                                                                                                                                                              |
| show the hostname - might indicate its purpose                                                                                                                          | `hostname`                                                                                                                                                                                                                              |
| list running processes                                                                                                                                                  | PowerShell: `Get-Process`<br>cmd: `tasklist`                                                                                                                                                                                            |
| list services whose credentials are stored in Windows credential manager (might reveal external services & usernames)                                                   | `cmdkey /list`                                                                                                                                                                                                                          |
| List installed security updates                                                                                                                                         | `Get-CimInstance -Class win32_quickfixengineering \| Where-Object { $_.Description -eq "Security Update" }`                                                                                                                             |
| List installed updates                                                                                                                                                  | `wmic qfe get Caption,Description,HotFixID,InstalledOn`                                                                                                                                                                                 |
| Get integrity level of current process                                                                                                                                  | use [[3 Tools/microsoft/Sysinternals#Process Explorer\|Process Explorer]]<br>use third party powershell modules: [NtObjectManager](https://www.powershellgallery.com/packages/NtObjectManager/1.1.33) --> `Get-NtTokenIntegrityLevel`<br> |

## Network

| Purpose                                          | Command                       |
| ------------------------------------------------ | ----------------------------- |
| list all network interfaces                      | `ipconfig /all`               |
| display routing table                            | `route print`                 |
| list active network connections and related PIDs | `netstat -ano`                |
| get process name of specified PID                | `tasklist /FI "PID eq <PID>"` |

### Relevant information:

- Are IPs set manually --> might be a server
- routing table might reveal other systems or network segments without creating noise
- Type and PID of services bound to network interface --> match services with [[#Installed Applications]]
- Services running only on localhost often have weaker security measures than external facing services.

## Installed Applications

32 bit software - based on registry:

```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*"
```

64 bit software - based on registry:

```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*"
```

**Hint:** To get only an overview, filter the output with `| select displayname`.

Also check Program Files in Downloads and root folder by [[#Search Files]]

**Then:**

- search [[1 Methods/Security-Testing/4 Execution/Using Public Exploits|Public Exploits]] for the installed software
- check for password managers to perform [[1 Methods/Security-Testing/8 Credential Access/Overview - 8 Credential Access|Credential Access]]

## Search Files

**Note:** the `-Recurse` flag in PowerShell and `/s` in cmd enable recursive searching

The following files might include sensitive information:

- [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
- configuration files of installed software: (weak) configurations, credentials
- .txt files: credentials, spontaneous notes of users
- password safe databases
- relevant filetypes: `*.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx,*.ini`

### Name-based - Quick Reference

| Goal                       | PowerShell                   | CMD                   |
| -------------------------- | ---------------------------- | --------------------- |
| Filter by extension        | `gci -Recurse -Filter *.txt` | `dir /si *.txt`       |
| Files only (no dirs)       | `gci -Recurse -File`         | `dir /si /a-d`        |
| Start from a specific path | `gci C:\MyFolder -Recurse`   | `dir C:\MyFolder /si` |

### Content-based - Quick Reference

**Quick Reference:**

| Goal                | PowerShell                                                 | CMD                                   |
| ------------------- | ---------------------------------------------------------- | ------------------------------------- |
| Search all files    | `gci -Recurse -File \| Select-String "searchterm"`         | `findstr /s /i "searchterm" *.*`      |
| Filter by extension | `gci -Recurse -Filter *.log \| Select-String "searchterm"` | `findstr /s /i "searchterm" *.log`    |
| Case-sensitive      | `Select-String "searchterm" -CaseSensitive`                | `findstr /s "term" *.*` (default)     |
| Show only filenames | `... \| Select-Object -ExpandProperty Path`                | `findstr /s /i /m "searchterm" *.*`   |
| Regex search        | `Select-String "searchterm\d+"`                            | `findstr /s /r "searchterm[0-9]" *.*` |

### cmd

eg. `dir /si [keyword] *.txt`

| Purpose                               | Option |
| ------------------------------------- | ------ |
| search current directories & sub-dirs | `/s`   |
| case in-sensitive search              | `/i`   |

### PowerShell

use `Get-ChildItem` or the short form `gci`

```powershell
Get-ChildItem -Path C:\ -Recurse -ErrorAction SilentlyContinue -Include "myfile.txt"
```

Use `?`and `*`as wildcards.

#### User files listing snippet

This snippet lists all directories in a users home folder, as well as their files in Document, Desktop and Downloads

```powershell
& { $ErrorActionPreference = 'SilentlyContinue'; Get-ChildItem "C:\Users" -Directory | ForEach-Object { $u = $_.FullName; Write-Host "`n=== $($_.Name) ===" -ForegroundColor Cyan; Write-Host "`n-- Home Folders --" -ForegroundColor Yellow; Get-ChildItem $u -Directory | ForEach-Object { Write-Host "  $($_.Name)" }; @("Documents","Desktop","Downloads") | ForEach-Object { $p = Join-Path $u $_; if (Test-Path $p -ErrorAction SilentlyContinue) { Write-Host "`n-- $_ --" -ForegroundColor Yellow; Get-ChildItem $p -Recurse | ForEach-Object { Write-Host "  $($_.FullName)" } } } } }
```

## Antivirus Enum

2 options: search for antivirus explicitely or list all running services and checking for antivirus

| Purpose                                                   | Command                                                |
| --------------------------------------------------------- | ------------------------------------------------------ |
| search for "windefend" service                            | `sc query windefend`                                   |
| list all active services                                  | `sc queryex type=service`                              |
| view running services (filter with `findstr "[keyword]"`) | `wmic service get name,displayname,pathname,startmode` |

## Command History

There are multiple logging mechanisms.

| Purpose                                                                                                                                                                                                                    | Command                                                                                                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Show PowerShells native history                                                                                                                                                                                            | `Get-History`                                                                                                                                                                                                                                                                                                                              |
| Show PSReadline history<br>(this is not cleared by the well-known `Clear-History` command)                                                                                                                                 | `cat (Get-PSReadlineOption).HistorySavePath`                                                                                                                                                                                                                                                                                               |
| Check Script Blog Logging records<br>See: [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.5&viewFallbackFrom=powershell-7.2) | 1. open Event Viewer<br>2. go to "Application and Services Logs" --> Microsoft --> Windows --> PowerShell or PowerShell-Core<br>3. Filter as described in [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.5&viewFallbackFrom=powershell-7.2) |

**Note:** Also [Transcript Files](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.host/start-transcript) might contain relevant information,

## Unattend Files

file name: Unattend.xml

helps sysadmins to set up the windows system, sometimes is left on teh system

may contain valuable info
