---
tags:
  - "#type/tech-specific" 
  - todo 
---

These files are expecially sensitive, since they can provide critical information to an attacker. Depending on your current privileges & configuration (issues) they may be accessible or not

## OS Independent

- SQLite Databases

## Webservers

| File | Description |
|----------|--------------|
| `/phpmyadmin.php` | gives info about database, system, etc... |

**Apache logs**

- on linux: `/var/log/apache2/access.log`
**XAMPP logs**
- xampp apache on windows: `C:\xampp\apache\logs\`

## Linux

| File                                                                                                                                                                                                                                | Description                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/etc/passwd`                                                                                                                                                                                                                       | user accounts, login shells - **readable by all users**<br>if writable, a user can be added                                                                       |
| `/etc/shadow`                                                                                                                                                                                                                       | password hashes                                                                                                                                                   |
| `/home/<user>/.ssh/known_hosts`<br>`/home/<user>/.ssh/authorized_keys`<br>`/home/<user>/.ssh/id_dsa`<br>`/home/<user>/.ssh/id_rsa`<br>`/home/<user>/.ssh/id_ecdsa`<br>`/home/<user>/.ssh/id_ed25519`<br>`/home/<user>/.ssh/id_xmss` | ssh keys, and other files also try keys with `-` instead of `_`                                                                                                   |
| `/etc/issue`                                                                                                                                                                                                                        | contains a message or system identification to be printed before the login prompt.                                                                                |
| `/etc/profile`                                                                                                                                                                                                                      | controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived |
| `/proc/version`                                                                                                                                                                                                                     | specifies the version of the Linux kernel                                                                                                                         |
| `/root/.bash_history`                                                                                                                                                                                                               | contains the history commands for root user                                                                                                                       |
| `/var/log/dmessage`                                                                                                                                                                                                                 | contains global system messages, including the messages that are logged during system startup                                                                     |

## Windows

| File                                  | Description                                                 |
| ------------------------------------- | ----------------------------------------------------------- |
| `\Windows\System32\drivers\etc\hosts` | readable by all users, good for testing directory traversal |
| `C:\boot.ini`                         | contains the boot options for computers with BIOS firmware  |
| `C:\inetpub\logs\LogFiles\W3SVC1\`    | Logs of IIS webserver                                       |
| `C:\inetpub\wwwroot\web.config`       | configs of an IIS webserver                                 |

- `C:\Users\Public\Documents\`: read & writable by all users
