---
tags:
  - "#type/tool"
  - "#attack/reconnaissance/active"
  - "#attack/lateral-movement"
  - "#attack/exfiltration"
Link: https://www.samba.org/samba/docs/current/man-html/smbclient.1.html
Purpose: smb client
---
# Info

connect to smb shares

# Usage

> [!HINT] smbclient´s options can be finicky
> Make sure to use the right format & options in the right order

`smbclient [options] //<IP>/[SHARE] <password>`

in smb client shell: `help` for available commands

| Option                | Purpose                                                                                                                        |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `--pw-nt-hash <hash>` | authenticate using NLTM hash - see [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash\|Pass the Hash]] |
| `-U`                  | User                                                                                                                           |
| `-L`                  | list shares                                                                                                                    |

# Snippets

## Pass the Hash

List smb shares using hash to authenticate

`smbclient -L <ip> -U <user>%<hash> --pw-nt-hash`
