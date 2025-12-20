---
tags:
  - "#type/tech-specific"
  - "#attack/defense-evasion"
---
# Fundamentals
Also see [[2 Tech-Specifics/OS/Antivirus & EDR Fundamentals|Antivirus & EDR Fundamentals]]

There are two categories:
1. [[#On-Disk Evasion]]
2. [[#In-Memory Evasion]]
Modern malware often operates in memory only and thus focuses on In-memory evasion. To successfully evade modern antivirus, usually a combination of multiple advanced techniques is needed.
## On-Disk Evasion
There are several techniques to evade antivirus on disk:
### Packers / Executable compression
Packers create an executable that is smaller, but functionally equivilant --> changes the signature.
(Not very useful nowadays)
### Obfuscators
Various operations are performed to change the code signature
- Inserting irrelevant instructions
- splitting & reordering functions
- modify the code in-memory
Not very effectivy against modern antivirus.
### Crypter
Encrypts major part of the software - encryption is done in memory --> less traces on disk.
## etc
Further techniques:
- anti reversing
- anti debugging
- virtual machine / emulation detection
## In-Memory Evasion
Process injection is a common technique for in memory evasion. Multiple sub-techniques exist.
**Ressources:**
- [MITRE Att@ck technique](https://attack.mitre.org/techniques/T1055/)
- https://www.elastic.co/blog/ten-process-injection-techniques-technical-survey-common-and-trending-process
### Remote Process Memory Injection
Inject a payload into another benign process memory and run it in a new thread. This is usually performed using [Windows APIs](https://en.wikipedia.org/wiki/Windows_API), e.g. through [[2 Tech-Specifics/OS/Windows/PowerShell|PowerShell]].
1. Get a process handle using `Open Proces`
2. Allocate Memory using `VirtualAllocEx`
3. Write the payload to the memory using `WriteProcessMemory`
4. Execute the payload using `CreateRemoteThread`
### DLL Injection
Load a malicous DLL from disk using `LoadLibrary`
### Reflective DLL Injection
Load malicous DLL from **memory**.
Ressource: https://andreafortuna.org//2017/12/08/what-is-reflective-dll-injection-and-how-can-be-detected/
### Process Hollowing
1. Create a benign process in suspended mode
2. Replace the memory image with the payload
3. Resume the process
Ressorce: https://www.ired.team/offensive-security/code-injection-process-injection/process-hollowing-and-pe-image-relocations
### Inline Hooking
Attempt to redirect execution flow to the payload, and then back to legitimate code. This is often done by [[2 Tech-Specifics/OS/Rootkits|Rootkits]]
# Pentesting

> [!Warning] Warning
> AV bypassing depends heavily on the used product and is a rapidly changing field. Finding a suitable bypass can be resource intensive & error prone.

## Testing Antivirus Evasion
1. Know the targets antivirus product.
	1. If you dont know the antivirus product, try harder.
	2. As a last resort, use e.g. [[3 Tools/Malware analysis/KleenScan|KleenScan]] to check your payload against popular antivirus products.
2. If possible, deploy the antivirus product yourself and check the payload against it.
	1. **Important:** Check if the antivirus sends samples of scanned artefacts - if possible disable it.
	2. If the target as sample submission enabled, also enable it for further testing

## Tools
Good commercial tool: [The Enigma Protector](https://www.enigmaprotector.com/en/home.html)
## amsi.fail (Obfuscation)
1. get amsi bypass from
https://amsi.fail/
2. https://github.com/danielbohannon/Invoke-Obfuscation

If the antivirus system is triggered --> analyse what part of the payload triggered it.
Useful Ressources:
- https://github.com/matterpreter/DefenderCheck
- https://github.com/rasta-mouse/ThreatCheck

## Thread Injection using PowerShell
Basic approach: 

# Hardening
