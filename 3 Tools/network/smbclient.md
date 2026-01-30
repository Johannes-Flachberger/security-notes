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

connect to [[2 Tech-Specifics/Network/Protocols/TCP 445 SMB|SMB]] shares

# Usage

> [!HINT] smbclient´s options can be finicky
> Make sure to use the right format & options in the right order. Sometimes it helps to double the `\`characters

`smbclient [options] //<IP>/[SHARE] -U <user> --password <password>`

| Option                  | Purpose                                                                                                                        |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `--pw-nt-hash <hash>`   | authenticate using NLTM hash - see [[2 Tech-Specifics/OS/Windows/Authentication Attacks Windows#Pass the Hash\|Pass the Hash]] |
| `-U <user>`             | User                                                                                                                           |
| `--password <password>` | password                                                                                                                       |
| `-L`                    | list shares                                                                                                                    |
| `-p <port>`             | port                                                                                                                           |
|                         |                                                                                                                                |

# Snippets

## List shares

`smbclient [-p <port>] -L //<ip> -U <user> --password <password>`

## Pass the Hash

List smb shares using hash to authenticate

`smbclient -L <ip> -U <user>%<hash> --pw-nt-hash`
