---
tags:
  - "#type/tech-specific"
---
# Fundamentals

There are several ways to "hijack" a service, i.e. modify its code to achieve code execution in the security context of the service.

# Pentesting

## Service Binary Hijacking

If permissions on a binary that is run by a service are not set restrictive enough, the binary can be replaced and gets run by the service user (usually with )

### Workflow

1. List running services and their executables:

```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName,StartMode | Where-Object {$_.State -like 'Running'}
```

2. List all information on a service:

```powershell
Get-CimInstance -ClassName win32_service | Select * | Where-Object {$_.Name -like '<service name>'}
```

Services with atypical / user-defined executables might be vulnerable.

3. Show privileges on executables `icacls "<path>"` or `Get-ACL`. Look for write (W) or full (F) privileges.
4. If required privileges are present, replace the service with another executable, e.g.
	- [[1 Methods/Security-Testing/12 Command and Control/Remote Shells|Remote Shells]]
	- [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#AddUser Snippet|add a user]]
5. If possible, manually restart the service, or reboot the machine if service StartMode is set to "auto" (requires `SeShutdownPrivilege`)

## DLL Hijacking

### Overwrite DLLs

The same approach as [[#Service Binary Hijacking]] but applied to DLLs.

### Search Order Hijacking

To achieve a DLL hijack, insert a malicious DLL in a higher position in the search order than the legitimate DLL is in.

#### Workflow

1. Enumerate DLLs and their position in the search order.
	- Typically [[3 Tools/microsoft/Sysinternals#ProcMon|ProcMon]] used to analyse an executable. - Since it requires admin privileges, mirror the target setup for preparation. ProcMon can be overwhelming. Filter for the target process name, the DLL name, take actions & relate the events to the actions.
2. Prepare a malicious DLL
	- See [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#DLLs|DLL Template]]
	- compile e.g. with [[3 Tools/compiler/mingw-w64|mingw-w64]]
3. Place DLL at the right location

#### DLL search order

If **SafeDllSearchMode** is enabled:

1. directory from which the application loaded.
2. The system directory. Use [GetSystemDirectory](https://docs.microsoft.com/en-us/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getsystemdirectorya) to get its path.
3. The 16-bit system directory.
4. The Windows directory. Use [GetWindowsDirectory](https://docs.microsoft.com/en-us/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getwindowsdirectorya) to get its path.
5. The current directory.
6. PATH directories. Note that this does not include the per-application path specified by the "App Paths" registry key.

If **SafeDllSearchMode** is disabled:

1. dir where application is loaded
2. current directory
3. system directory
4. 16-bit system directory
5. windows directory
6. PATH directories

## Unquoted Service Path

If the path of a service executable includes spaces and is not placed in quotes, it is unlcear to Windows where the path ends and where the next argument begins. --> Windows tries to call each fragment that is separated by a space, starting from the left.

**Example:**

The path is: `C:\Program Files\My Service\service.exe.`

Windows would try to call `C:\Program.exe` and `C:\Program Files\My.exe`.

You can put a malicious executable in a place where windows tries to call it before the legitimate executable.

**Prerequisites**

1. Being able to write to a folder within the path of the service executable.
2. Being able to restart the service (or reboot the machine - requires `SeShutdownPrivilege`)

### Workflow

1. find service with unquoted path
	- `wmic service get name,pathname,startmode`
		- it can make the search easier to exclude services in the windows folder: `| findstr /i /v "C:\Windows\\"` (run in [[cmd]] shell)
		- filter for paths without quotes: `| findstr /i /v """`
2. check privileges on path:
	- eg. `.\accesschk64.exe /accepteula -uwdq "<path>"`
	- eg. `icacls "<path>"`
3. insert a malicious executable
	- [[1 Methods/Security-Testing/12 Command and Control/Remote Shells|Remote Shells]]
	- [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#AddUser Snippet|add a user]]
4. start/restart service
	- `sc start [service name]`

# Hardening
