---
tags:
  - "#type/tool"
Link: https://github.com/ShawnDEvans/smbmap
Purpose: smb enumeration tool with remote file searching features
---
# Info

# Usage

**Example:** List files recursively

`smbmap -u <user> -p <password> -H <host> -r /Users/ --depth 3`

**Example:** search for text files recursively

`smbmap -u <user> -p <password> -H <host> -r 'C$' -A '\.txt$' --depth 10`

| Option          | Purpose                                                         |
| --------------- | --------------------------------------------------------------- |
| `-r <path>`     | list files recursively, starting at `<path>`                    |
| `--depth <num>` | recursion depth                                                 |
| `--download`    | download a file                                                 |
| `-A <pattern>`  | Search for and auto-download files that match the regex pattern |

> [!Hint]
> Recursive file listing can take a long time

# Snippets
