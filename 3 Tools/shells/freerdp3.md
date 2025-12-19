---
tags:
  - type/tool
  - attack/command-and-control
  - attack/exfiltration
Link: https://www.kali.org/tools/freerdp3/
Purpose: remote desktop protocol (RDP) client for X11 environments
---
# Info
open source remote desktop client
apart from `xfreerdp3`, also check out the other clients
# Usage
Example with good default options:

```sh
xfreerdp3 /dynamic-resolution +clipboard /toggle-fullscreen /compression /network:auto +fonts /auto-reconnect /cert:ignore /size:1920x1080 /scale:180 /v:192.168.x.x /u:<user> /p:<password>
```

| Option                                  | Purpose                                                                                                |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `/cert:ignore`                          | skip certificate validation                                                                            |
| `/scale:<scaling>`                      | set scaling factor, 180 works well on hiDPI screens                                                    |
| `+drive:<remote_folder>,<local_folder>` | make a local folder available on the target - remote folder will be available in `Network -> tsclient` |
