tags: #type/theory #tech/OS/linux #tactic/privilege-escalation 

---

useful commands for manual enumeration for privesc
- `id [user]`: show user&group info 
- `hostname` command may show valuable information about the role of the machine
- `uname -a`: to show kernel info, are there kernel vulns?
- `/proc/version`: may give info on kernel and if compiler is installed
- `/etc/issue`: may give system info
- `ps aux`: show processes for all users
- `env`: show environment variables, eg PATH may contain useful compiler/scripting language
- `/etc/passwd`: info on users, groups,... eg. grep for "home" to fin real users, not just service users
- `ifconfig`: info about network interfaces

## netstat
[[3_Tools/netstat]]
## find files
- `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
- `find / -perm a=x`: find executable files
- `find /home -user frank`: find all files for user “frank” under “/home”
- `find / -mtime 10`: find files that were modified in the last 10 days
- `find / -atime 10`: find files that were accessed in the last 10 day
- `find / -cmin -60`: find files changed within the last hour (60 minutes)
- `find / -amin -60`: find files accesses within the last hour (60 minutes)
- `find / -size 50M`: find files with a 50 MB size

**writeable files/folders**
- `find / -writable -type d 2>/dev/null` : Find world-writeable folders
- `find / -perm -222 -type d 2>/dev/null`: Find world-writeable folders
- `find / -perm -o w -type d 2>/dev/null`: Find world-writeable folders
- `find / -writable 2>/dev/null`: search for writeable folders
- `find / -writable 2>/dev/null | cut -d "/" -f 2,3 | grep -v proc | sort -u`: search for subdirectories of writeable folders:

- `find / -perm -o x -type d 2>/dev/null`: find world-executabe folders
    