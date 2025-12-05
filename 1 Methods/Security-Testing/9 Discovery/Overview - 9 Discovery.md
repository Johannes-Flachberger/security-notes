#todo 
When we already are inside the targeted infrastructure, we either have a good C2 framework running, or must use tools that are available on the machine we are on. This limits the available techniques.

Very helpful ressource: "Living off the land binaries, scripts and libraries" (LOLBAS): https://lolbas-project.github.io/#

# Shortlist of tools
- DNS lookup with [[3 Tools/passive recon/DNS enumeration Tools|nslookup]]
- Port scan with [[3 Tools/shells/Netcat|Netcat]]
- Manual SMTP enumeration with [[2 Tech-Specifics/Network/Protocols/TCP 23 Telnet|TCP 23 Telnet]]
- Port scan with [[2 Tech-Specifics/OS/Windows/PowerShell|PowerShell]]
- SMB enum on windows: [[3 Tools/network/SMB tools#net view|net view]]
# Tech-Specific Attack Vectors
```query
tag:#tactic/discovery  tag:#type/tech-specific 
```
# Tools
```query
tag:#tactic/discovery tag:#type/tool 
```