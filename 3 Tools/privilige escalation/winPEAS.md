---
tags:
  - "#type/tool"
  - "#attack/privilege-escalation"
Link: https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS
Purpose: auto privesc enum on windows
---
# Info

used to scan windows machines automatically for privesc opportunities

**is detected by windows defender**

# Usage

**Example:** `.\winPEASx64.exe all -network="<ip1>,<ip2>,..." log=winpeas.log`

| Option       | Purpose                              |
| ------------ | ------------------------------------ |
| `-h`         | show help                            |
| `log=<path>` | log to file - e.g. `log=winPEAS.log` |
