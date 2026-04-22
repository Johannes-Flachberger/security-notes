---
tags:
  - "#type/tech-specific" 
  - "#attack/execution/server-side" 
---
# Fundamentals

execute shell commands on the webserver

-> you can try to steal information, open a reverse shell,...

**Attack Surface:**

- Every time when a web application needs to interact with the operating system and commands are used without proper sanitation.
- E.g. File uploads

## Two Types: Blind & Verbose

### Blind Command Injection

- webapp does not output message
- use payloads that cause time delay and check if the website hangs for that amount of time eg. `ping` or `sleep` - also see [[3 Tools/shells/bash|bash]]
- redirect output to eg. a file using `>`

### Verbose Command Injection

webapp gives output - this is generally much easier to handle

# Pentesting

## Filter Bypassing

sometimes a specific command is allowed, zB. ls - we can the poke around to see if we can

- use arguments to e.g. show the version (and possibly the infer the OS)
- concatenate another command with `;` or `&&`
Bypass filters using [[2 Tech-Specifics/Web/Attacks - Web/Injection Attacks/Filter Bypassing - Injection|Filter Bypassing - Injection]]

## Get Environment Info

detect if you are in cmd or PowerShell:

```powershell
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```

## Useful Payloads

- [[1 Methods/Security-Testing/12 Command and Control/Remote Shells|Remote Shells]]
- <https://github.com/payloadbox/command-injection-payload-list>
- <https://hackersonlineclub.com/command-injection-cheatsheet/>

## Tricks

- with reverse shells, sometimes things dont work as expected, e.g. the nc -e option might not work. In this case try different commands/ variations of the payload
- avoid special characters as mus as possible, since they might influence parsing or might be filtered by a WAF - e.g. use [[3 Tools/web/wget|wget]] to download payloads to a target.

# Hardening

**input sanitisation**
