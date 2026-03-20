---
tags:
  - "#type/tool"
Link:
Purpose: network management
---
# Info

windows built in network management tool

# Usage

`net help`: show help menu

## SMB enumeration

smb enumeration on windows - lists domains, resources, and computers belonging to a given host.

e.g. `net view \\dc01 /all`

| Option | Purpose |
|----------|--------------|
| `/all` | lists administrative shares too |
| `/all` | Lists all shares, including administrative shares. |
| `/domain` | Lists all domains/workgroups on the network. |
| `/domain:<DomainName>` | Lists all computers in the specified domain. |
| `net view \\SERVER1` | List all shares on the server |

## Service Management

| Command               | Purpose       |
| --------------------- | ------------- |
| `net stop <service>`  | stop service  |
| `net start <service>` | start service |

# Snippets
