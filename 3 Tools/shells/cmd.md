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

## Useful options

| Purpose                               | Option |
| ------------------------------------- | ------ |
| search current directories & sub-dirs | `/s`   |
| case in-sensitive search              | `/i`   |

## Useful Commands

| Command                                 | Purpose                                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------ |
| `type`                                  | print file content - for large files use `more`                                            |
| `cls`                                   | clear command prompt                                                                       |
| `net`                                   | see [[3 Tools/network/net (windows built-in)\|net (windows built-in)]]                     |
| `icacls`                                | show permissions of a file or folder                                                       |
| `where [options] <directory> <pattern>` | find files<br>use option `/r` for recursive search<br>e.g. `where /r C:\ report.*`         |
| `where <command>`                       | check if a command is available, and show its executable location                          |
| `reg`                                   | interact with the registry                                                                 |
| `runas /user:<user> <command> `         | run command as another user<br>**Note:** Does not grant admin privileges if UAC is active. |
| `shutdown /r /t 0`                      | reboot the machine immediately                                                             |

# Snippets

## Enumeration

Also see [[2 Tech-Specifics/OS/Windows/Basic Enumeration - Windows|Basic Enumeration - Windows]]

| Command                                         | Purpose                                                                                                                 |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `sc queryex type=service state=all`             | show all available services                                                                                             |
| `netsh firewall show state`                     | show firewall state                                                                                                     |
| `netsh firewall show config`                    | show firewall config                                                                                                    |
| `wmic /node:"" product get name,version,vendor` | show details of installed software                                                                                      |
| `wmic useraccount get name,sid`                 | show login names and SIDs of users                                                                                      |
| `dir \\<ip>\<share>`                            | list files on smb share - also see [[2 Tech-Specifics/OS/Windows/Fundamentals - Windows#UNC Paths\|Windows fundamentals]] |

## Automate command prompt responses

In non-tty where you cannot respond to command prompts, pipe the answer into the command like this:

```powershell
cmd.exe /c echo y | <command>
```

## File Searching

**Example** `dir /si [keyword] *.txt`

**Name-based**

| Command               | Purpose                    |
| --------------------- | -------------------------- |
| `dir /si *.txt`       | Filter by extension        |
| `dir /si /a-d`        | Files only (no dirs)       |
| `dir C:\MyFolder /si` | Start from a specific path |

**Content-based**

| Command                               | Purpose             |
| ------------------------------------- | ------------------- |
| `findstr /s /i "searchterm" *.*`      | Search all files    |
| `findstr /s /i "searchterm" *.log`    | Filter by extension |
| `findstr /s "term" *.*` (default)     | Case-sensitive      |
| `findstr /s /i /m "searchterm" *.*`   | Show only filenames |
| `findstr /s /r "searchterm[0-9]" *.*` | Regex search        |
