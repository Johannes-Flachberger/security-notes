---
tags:
  - type/tech-specific 
  - tactic/execution/server-side 
---
# Fundamentals
execute shell commands on the webserver
-> you can try to steal information, open a reverse shell,...
## Entrypoints
Every time when a web application needs to interact with the operating system and commands are used without proper sanitation.
For example:
- File uploads
## Two types: blind & verbose
### Blind Command Injection
- webapp does not output message
- use payloads that cause time delay and check if the website hangs for that amount of time eg. `ping` or `sleep` - also see [[3 Tools/shells/bash|bash]]
- redirect output to eg. a file using `>` 
### Verbose Command Injection
webapp gives output
# Pentesting
## Filter bypassing
sometimes a specific command is allowed, zB. ls - we can the poke around to see if we can
- use arguments to e.g. show the version (and possibly the infer the OS)
- concatenate another command with `;` or `&&` 
Bypass filters using [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Filter Bypassing - Injection|Filter Bypassing - Injection]]
## Get environment info
detect if you are in cmd or PowerShell:
```powershell
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```
## Useful payloads
- [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Remote Shells]]
- https://github.com/payloadbox/command-injection-payload-list
- https://hackersonlineclub.com/command-injection-cheatsheet/

## Tricks
- with reverse shells, sometimes things dont work as expected, e.g. the nc -e option might not work. In this case try different commands/ variations of the payload
# Hardening
**input sanitisation**

