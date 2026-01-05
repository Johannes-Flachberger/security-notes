---
tags:
  - "#type/tool"
Link: https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands
Purpose: windows command prompt
---
# Info

See link for full list of commands.

# Usage

for help menu of each command: `/?`

## Useful Commands

| Command                                 | Purpose                                                                                         |
| --------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `type`                                  | print file content - for large files use `more`                                                 |
| `hostname`                              | show hostname                                                                                   |
| `ipconfig`                              | show network adress settings                                                                    |
| `netstat`                               | display protocol statistics                                                                     |
| `cls`                                   | clear command prompt                                                                            |
| `net`                                   | manage network resources; help menu: `net help`                                                 |
| `icacls`                                | show permissions of a file or folder                                                            |
| `where [options] <directory> <pattern>` | find files<br>use option `/r` for recursive search<br>e.g. `where /r C:\ report.*`              |
| `ver`                                   | show windows version                                                                            |
| `systeminfo`                            | show detailed system info                                                                       |
| `reg`                                   | interact with the registry                                                                      |
| `runas /user:<user> <command> `         | run with command as another user<br>**Note:** Does not grant admin privileges if UAC is active. |
| `shutdown /r /t 0`                      | reboot the machine immediately                                                                  |

## Service Management

| Command               | Purpose       |
| --------------------- | ------------- |
| `net stop <service>`  | stop service  |
| `net start <service>` | start service |

# Snippets

## Enumeration

Also see [[2 Tech-Specifics/OS/Windows/Privilege Escalation Windows/Manual Enumeration Windows|Manual Enumeration Windows]]

| Command                                         | Purpose                                                                                                                 |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `sc queryex type=service state=all`             | show all available services                                                                                             |
| `netsh firewall show state`                     | show firewall state                                                                                                     |
| `netsh firewall show config`                    | show firewall config                                                                                                    |
| `wmic /node:"" product get name,version,vendor` | show details of installed software                                                                                      |
| `wmic useraccount get name,sid`                 | show login names and SIDs of users                                                                                      |
| `dir \\<ip>\<share>`                            | list files on smb share - also see [[2 Tech-Specifics/OS/Windows/Fundamentals Windows#UNC Paths\|Windows fundamentals]] |
