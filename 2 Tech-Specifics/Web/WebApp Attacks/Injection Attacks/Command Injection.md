**Tags:** #type/tech-specific #tactic/execution 

---
# Fundamentals
execute shell commands on the webserver
-> you can try to steal information, open a reverse shell,...
## Two types: blind & verbose
### Blind Command Injection
- webapp does not output message
- use payloads that cause time delay and check if the website hangs for that amount of time eg. `ping` or `sleep` - also see
- redirect output to eg. a file using `>` 
### Verbose Command Injection
webapp gives output
# Pentesting
Bypass filters using [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/Filter Bypassing|Filter Bypassing]]
## Useful payloads
https://github.com/payloadbox/command-injection-payload-list
https://hackersonlineclub.com/command-injection-cheatsheet/
## Tricks
- with reverse shells, sometimes things dont work as expected, e.g. the nc -e option might not work. In this case try different commands/ variations fo the payload
# Hardening
**input sanitisation**

