**Tags:** #type/method #tactic/command-and-control 

---
**There are 2 types of remote shells:**
- Reverse shells: target connects to your machine - usually better
- Bind shells: your machine connects to target
# reverse shell receivers
- [[3 Tools/shells/Netcat|Netcat]]: simple, by default very unstable
- [[3 Tools/shells/powercat|powercat]]: basically Netcat for [[2 Tech-Specifics/OS/Windows/PowerShell|PowerShell]]
- [[3 Tools/shells/Socat|Socat]]: powerful, but difficult to use
- [[3 Tools/exploitation_frameworks/Metasploit/Overview - Metasploit|Metasploit - multi/handler module]]: very stable
- [[3 Tools/exploitation_frameworks/Metasploit/meterpreter|meterpreter]]: powerfull listener & client
# Payloads
- [[2 Tech-Specifics/OS/Windows/PowerShell#Reverse Shell Payloads|PowerShell]]
- [[3 Tools/shells/bash#Simple Reverse Shell|bash]]
# Payload sources
- webshells on kali: `/usr/share/webshells/`
- [Payload all the things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)
- [Pentestmonkey](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
- [[3 Tools/bruteforce/SecLists|SecLists]]
- [[3 Tools/exploitation_frameworks/Metasploit/msfvenom|msfvenom]]: Generate Payloads 
# general tricks:
manually adjust tty size, to be able to use editors,...:
`stty -a` for tty info (run in your own terminal)
then set the same values for remote shell on target machine:
`stty rows <number>`  
and
`stty cols <number>`
# Stabilisation
- [[2 Tech-Specifics/OS/Windows/Reverse Shell Stabilisation|Reverse Shell Stabilisation - Windows]]
- [[2 Tech-Specifics/OS/Linux/Reverse Shell Stabalisation|Reverse Shell Stabalisation - Linux]]

