---
tags:
  - "#type/tool"
  - "#attack/reconnaissance/active"
  - "#attack/exfiltration"
  - "#attack/discovery"
Link:
Purpose: Tool collection for SMB
---
# Enumeration

## enum4linux

enumerate smb infos, eg. different shares

`enum4linux <options> [ip]`

eg: `enum4linux -a [IP] | tee enum4linux.log`

`-a` to enumerate all infos

if you want to enumerate multiple ips:

- put ips into a file, one each line
- `xargs -n 1 enum4linux -a < targets.txt`

## Net view

smb enumeration on windows

lists domains, resources, and computers belonging to a given host.

e.g. `net view \\dc01 /all`

| Option | Purpose |
|----------|--------------|
| `/all` | lists administrative shares too |
| `/all` | Lists all shares, including administrative shares. |
| `/domain` | Lists all domains/workgroups on the network. |
| `/domain:<DomainName>` | Lists all computers in the specified domain. |
| `net view \\SERVER1` | List all shares on the server |

### Nbtscan

e.g. `nbtscan -r 192.168.50.0/24`

`-r` sets originating udp port to 137

# Exfiltration

## Smbget

download files from SMB shares

recursively download whole share: `smbget -R smb://<ip>/<sharename>`
