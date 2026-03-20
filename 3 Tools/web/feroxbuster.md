---
tags:
  - "#type/tool"
Link: https://feroxbuster.com/
Purpose: recursive directory enumeration
---
# Info

less flexible than [[3 Tools/web/ffuf|ffuf]] or [[3 Tools/web/gobuster|gobuster]], but it has some outstanding features:

- recursive directory enumeration
- save and resume execution state
- exclude based on regex patterns

# Usage

**Example:** `feroxbuster -u <host> -t 100 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

| Option     | Purpose                                                |
| ---------- | ------------------------------------------------------ |
| `-t <num>` | number of threads                                      |
| `-d <num>` | recursion depth (0 is infinite)                        |
| `--smart`  | enable auto tune, word collection and collect backups  |

# Snippets
