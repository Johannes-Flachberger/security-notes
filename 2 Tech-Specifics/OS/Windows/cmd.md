---
tags:
  - "#type/tool"
Link:
Purpose:
---
# Info

Also see [[2 Tech-Specifics/OS/Windows/Enumeration/cmd Enumeration Cheat Sheet|cmd Enumeration Cheat Sheet]]

# Usage

for help menu of each command: `/?`

## Useful Commands

| Command                                 | Purpose                                                                                |
| --------------------------------------- | -------------------------------------------------------------------------------------- |
| `type`                                  | print file content - for large files use `more`                                        |
| `hostname`                              | show hostname                                                                          |
| `ipconfig`                              | show network adress settings                                                           |
| `netstat`                               | display protocol statistics                                                            |
| `cls`                                   | clear command prompt                                                                   |
| `net`                                   | manage network resources; help menu: `net help`                                        |
| `icacls`                                | show permissions of a file or folder                                                   |
| `where [options] <directory> <pattern>` | find files<br>- use option `/r` for recursive search<br>- e.g. `where /r C:\ report.*` |
| `ver`                                   | show windows version                                                                   |
| `systeminfo`                            | show detailed system info                                                              |
| `reg`                                   | interact with the registry                                                             |

# Snippets

| Command | Purpose |
|----------|--------------|
| `sc queryex type=service state=all` | show all available services |
| `netsh firewall show state` | show firewall state |
| `netsh firewall show config` | show firewall config |
| `wmic /node:"" product get name,version,vendor` | show details of installed software |
| `wmic useraccount get name,sid` | show login names and SIDs of users |
