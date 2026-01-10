---
tags:
  - "#type/method" 
  - "#attack/command-and-control" 
---
**There are 2 types of remote shells:**
- Reverse shells: target connects to your machine - usually better
- Bind shells: your machine connects to target

# Reverse Shell Receivers

- [[3 Tools/shells/Netcat|Netcat]]: simple, by default very unstable
- [[3 Tools/shells/powercat|powercat]]: basically Netcat for [[3 Tools/shells/PowerShell|PowerShell]]
- [[3 Tools/shells/Socat|Socat]]: powerful, but difficult to use
- [[3 Tools/exploitation frameworks/Metasploit/Overview - Metasploit|Metasploit - multi/handler module]]: very stable
- [[3 Tools/exploitation frameworks/Metasploit/meterpreter|meterpreter]]: powerfull listener & client
- [[3 Tools/network/tunneling/dnscat2|dnscat2]]: remote shell using dns (requires dnscat2 client)

# Payloads

**Note:** When using a payload inside a webshell, [[2 Tech-Specifics/Web/encodings#URL|URL encode]] the payload properly.
- [[3 Tools/shells/PowerShell#Reverse Shell Payloads|PowerShell]]
- [[3 Tools/shells/bash#Simple Reverse Shell|bash]]

# Payload Sources

- webshells on kali: `/usr/share/webshells/`
- [Payload all the things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)
- [Pentestmonkey](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
- [[3 Tools/bruteforce/SecLists|SecLists]]
- [[3 Tools/exploitation frameworks/Metasploit/msfvenom|msfvenom]]: Generate Payloads

# General Tricks:

manually adjust tty size, to be able to use editors,...:

`stty -a` for tty info (run in your own terminal)

then set the same values for remote shell on target machine:

`stty rows <number>`

and

`stty cols <number>`

# Stabilisation

- [[2 Tech-Specifics/OS/Windows/Reverse Shell Stabilisation|Reverse Shell Stabilisation - Windows]]
- [[2 Tech-Specifics/OS/Linux/Reverse Shell Stabalisation|Reverse Shell Stabalisation - Linux]]
