---
tags:
  - "#type/tool" 
  - "#attack/credential-access" 
Link: https://www.kali.org/tools/hydra/
Purpose: brute force network protocol logins
---
# Info

supports more than 50 Protocols, including Telnet, RDP, SSH, FTP, HTTP, HTTPS, SMB

# Usage

`hydra -l [username] -P [wordlist path] [server] [service]`

eg. `hydra -t 4 -l [user] -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp`

| Option                    | Purpose                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------ |
| `-t 4`                    | Number of parallel connections per target                                            |
| `-l [user]`               | specify one user                                                                     |
| `-L [userfile]`           | specify file of usernames                                                            |
| `-P [path to dictionary]` | file of possible passwords                                                           |
| `-p`                      | give one specific password                                                           |
| `-vV`                     | Sets verbose mode to very verbose, shows the login+pass combination for each attempt |
| `[machine IP]`            | The IP address of the target machine                                                 |
| `-s [PORT]`               | set port                                                                             |
| `[service]`               | Sets the protocol                                                                    |
| `-d`                      | debug - print more info about whats going on                                         |
| `http-post-form`          | see [[#Attack Web-Logins]]                                                           |

## Modules

For more complex syntax or login forms, hydra has specific modules. E.g. `http-post-form` or `http-get`

Get list of modules: `hyda -h` --> section "Supported services"

Get module help: `hydra <module> -U`

## Attack Web-Logins

Requires some setup. You need:

- The path to the login form (`<path>`)
- The body of a valid request - e.g. capture it with [[3 Tools/web/Burp Suite|Burp Suite]] (`<request_body>`)
- A string to identify a failed login (`<condition_string>`)
	- Hydra searches for the string, and if found it is considered a failed login.
	- Avoid keywords such as "username" and "password" in the condition string.
Use `^USER^` and `^PASS^` as placeholder for wordlist values.

### POST Forms

Syntax: `http-post-form "<path>:<request_body>:<condition_string>"

Example: `http-post-form "/login.php:&user=^USER^&pass=^PASS^:Login failed."`
