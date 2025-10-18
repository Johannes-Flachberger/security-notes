**Tags:** #type/tech-specific #todo 

---
These files are expecially sensitive, since they can provide critical information to an attacker. Depending on your current privileges & configuration (issues) they may be accessible or not
## OS independent
- SQLite Databases
### Webservers
- `/phpmyadmin.php`: gives info about database, system, etc...
- `/var/log/apache2/access.log`: the accessed requests for Apache  webserver
## Linux
- `/etc/passwd`: user accounts, login shells - readable by all users
- `/etc/shadow`: password hashes
- `/home/<user>/.ssh/`: ssh keys, known hosts
	- e.g. `.../.ssh/id_rsa
- `/etc/issue`: contains a message or system identification to be printed before the login prompt. 
- `/etc/profile`: controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived
- `/proc/version`: specifies the version of the Linux kernel 
- `/root/.bash_history`: contains the history commands for root user 
- `/var/log/dmessage`: contains global system messages, including the messages that are logged during system startup 
## Windows
- `\Windows\System32\drivers\etc\hosts`: readable by all users, good for testing directory traversal
- `C:\boot.ini`: contains the boot options for computers with BIOS firmware
- `C:\inetpub\logs\LogFiles\W3SVC1\`: Logs of IIS webserver
- `C:\inetpub\wwwroot\web.config`: configs of an IIS webserver
# What to look for generically




