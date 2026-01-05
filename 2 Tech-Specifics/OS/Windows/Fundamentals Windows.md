---
tags:
  - "#type/tech-specific"
---
# Windows Management Tools

- **Run things**
	- use the `run` dialog
- **computer management**
	- utility: `compmgmt.msc`
	- access all the important utilities for managing the system.
- **User and Group management**
	- run `lusrmgr.msc`
- **System Configuration**
	- utility: `msconfig`
	- local admin rights needed
- **task manager**
	- `taskmgr`

# UNC Paths

See: [Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/standard/io/file-path-formats#unc-paths)

Universal naming convention (UNC) paths are used to access network ressources using [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|SMB]]. They can be used and exploited at many different places. E.g.:

- [[3 Tools/shells/cmd|cmd]]
- [[2 Tech-Specifics/Web/WebApp Attacks/Web Upload Vulnerabilities|Web Upload Vulnerabilities]]
- [[2 Tech-Specifics/Web/WebApp Attacks/Directory Traversal|Directory Traversal]]

Further reading: [https://www.netspi.com/blog/technical-blog/network-pentesting/10-places-to-stick-your-unc-path/](https://www.netspi.com/blog/technical-blog/network-pentesting/10-places-to-stick-your-unc-path/)

# Hash Sources

Windows uses NTLM hashes - also see [[2 Tech-Specifics/_Other/Cryptography/Hashing fundamentals|Hashing fundamentals]]

## SAM

Hashes of local users are stored in the Security Account Manager (SAM) at `C:\Windows\system32\config\sam`. Several protections are applied on the database file.

## LSASS

The Local Security Authority Subsystem (LSASS) is the windows process that handles everything related to authentication.

Pre Windows 10: Hashes of both local users and logged-in domain users can be extracted from its memory (privileges required!)

Since Windows 10: [[#Windows Credential Guard]] protects secrets in LSASS memory.

# Named Pipes & RPC

## Named Pipes

See [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/ipc/named-pipes)

A server hosts a named pipe. One or multiple (remote and local) clients can connect to it to exchange information.

## RPC

See [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/rpc/rpc-start-page)

# Access Control Mechanisms

## Accounts & Privilege Levels

- **Administrator (local):** This is the user with the most privileges.
- **Standard (local):** These users can access the computer but can only perform limited tasks. Typically these users can not make permanent or essential changes to the system.
- **Guest:** This account gives access to the system but is not defined as a user.
- **Standard (domain):** Active Directory allows organizations to manage user accounts. A standard domain account may have local administrator privileges.
- **Administrator (domain):** Could be considered as the most privileged user. It can edit, create, and delete other users throughout the organization's domain.
- **SYSTEM account:** Kernel-level privileges - you cant log in, but it is used by services installed on the machine

## SIDs

SIDs are the primary identifier of users & groups of users on windows. It encodes various pieces of information, such as the domain, if the user is local or a domain user, etc. Example SID: `S-1-0-0`

In depth explanation: [Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-identifiers)

For local users, the last part starts with 1000 --> `S-1-5-21-948155058-1001` would be the second local user.

Useful SIDs for privilege escalation:

```
S-1-0-0                       Nobody        
S-1-1-0	                      Everybody
S-1-5-11                      Authenticated Users
S-1-5-18                      Local System
S-1-5-domainidentifier-500    Administrator
```

## Access Tokens

Define the security context of a user & process. When a process is started, it usually inherits the access token of the user who starts it / the parent process.

Access tokens include:  

- user SID
- SIDs of groups the user belongs to
- user & group privileges
- etc.

In depth explanation: [Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/secauthz/access-tokens)

[Impersonation Tokens](https://learn.microsoft.com/en-us/windows/win32/secauthz/impersonation-tokens) are used to grant a process a different security context than the parent process has.

## Mandatory Integrity Control (MIC)

This mechanisms runs in parallel to privilege levels and ensures that processes with a low integrity level cannot access objects with a high integrity level.

Integrity Levels:

- System – Highly trusted system processes in user-mode (e.g., `Winlogon`, `LSASS`)
- High – processes running with admin privileges
- Medium – standard user processes (default)
- Low – sandboxed or restricted processes (e.g., browsers)
- Untrusted – Rarely used; for highly restricted unverified sources

In-depth explanation:

- [Microsoft Learn - MIC](https://learn.microsoft.com/en-us/windows/win32/secauthz/mandatory-integrity-control)
- [Microsoft Learn - Integrity Levels](https://learn.microsoft.com/en-us/previous-versions/dotnet/articles/bb625963(v=msdn.10))

Check integrity levels of users with `whoami`and of files with `icacls`.

## UAC

Processes run with standard privileges by default, also if started by an admin user. To run with admin privileges, the user must explicitly request that.

See: [Microsoft Learn](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/)

# Security Measures

## Windows Credential Guard

Windows Credential Guard protects cached domain account hashes (but not local account hashes) using the [[#Virtual Secure Mode (VSM)]]. With Windows Credential Guard, LSASS becomes only a gateway to LSAISO.exe (also called LSA Isolated) which runs in VTL1. --> Cached hashes cannot directly accessed by the OS anymore, e.g. by reading the memory.

Further reading: [https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/how-it-works]()

## Virtual Secure Mode (VSM)

Reference: [https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/tlfs/vsm]()

The VSM is enabled using **Virtualisation Based Security (VBS)**. VBS creates an execution environment separate from the Kernel by Running Hyper-V directly on hardware.

--> Even with SYSTEM user can only access the this execution environment in a restricted way through the hypervisor.

VSM defines several **Virtual Trust Levels (VTLs)**.

- **VTL0:** Contains the normal kernel and user mode processes
- **VTL1:** Contains the isolated environment, often calles just "VMS"

VTL1 is used for various security functions, e.g. the [[#Windows Credential Guard]]

# Authentication Protocols

## NTLMv1

Challenge - response based authentication protocol. Uses the NT hash as long-term secret. It is prone to multiple attacks, such as:

- [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash|Pass the Hash]]
- replay
- spoofing, etc.

## NTLMv2

Improvement of NTLMv1. Adds a client challenge to prevent server spoofing. Also has protection against replay attacks. [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash|Pass the Hash]] is still possible.

## Kerberos

#todo

# DLLs

See: https://learn.microsoft.com/en-us/troubleshoot/windows-client/setup-upgrade-and-drivers/dynamic-link-library#the-dll-entry-point

The `DllMain`function is the entrypoint of a DLL. Based on the context, one of the 4 cases of the switch statement is selected (See comments in the code snippet.)

For pentesting purposes, code is typically added to the "Attached" cases, to e.g.

- create a new user
- open a [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Remote Shell]]

DLL Code example from [Microsoft](https://learn.microsoft.com/en-us/troubleshoot/windows-client/setup-upgrade-and-drivers/dynamic-link-library#the-dll-entry-point):

```c++
#include <windows.h>

BOOL APIENTRY DllMain(
HANDLE hModule,// Handle to DLL module
DWORD ul_reason_for_call,// Reason for calling function
LPVOID lpReserved ) // Reserved
{
    switch ( ul_reason_for_call )
    {
        case DLL_PROCESS_ATTACHED: // A process is loading the DLL.
        break;
        case DLL_THREAD_ATTACHED: // A process is creating a new thread.
        break;
        case DLL_THREAD_DETACH: // A thread exits normally.
        break;
        case DLL_PROCESS_DETACH: // A process unloads the DLL.
        break;
    }
    return TRUE;
}

```

**Note:** Depending on the version, instead of `..._ATTACHED` the right macro is `..._ATTACH`.

# AddUser Snippet

c code snippet to add a user in windows:

```c
#include <stdlib.h>

int main ()
{
  int i;
  
  i = system ("net user dave2 password123! /add");
  i = system ("net localgroup administrators dave2 /add");
  
  return 0;
}
```
