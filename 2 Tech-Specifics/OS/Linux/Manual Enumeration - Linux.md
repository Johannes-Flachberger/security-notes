---
tags:
  - "#type/tech-specific"
  - "#attack/privilege-escalation"
  - "#attack/discovery"
  - "#attack/collection"
---
# Fundamentals

See [[2 Tech-Specifics/OS/Linux/Privilege Escalation - Linux/Overview - Privilege Escalation - Linux|Overview - Privilege Escalation - Linux]] and [[2 Tech-Specifics/OS/Linux/Fundamentals - Linux|Fundamentals - Linux]]

# Pentesting

## Users & Groups

| Command       | Purpose                                                                                        |
| ------------- | ---------------------------------------------------------------------------------------------- |
| `id [user]`   | show user & group info                                                                         |
| `/etc/passwd` | info on users, groups,... eg. grep for "home" to fin real users, not just service users        |
| `env`         | show all set environment variables<br>- eg PATH may contain useful compiler/scripting language |
| `sudo -l`     | list sudo privileges of current user<br>**Prerequisite:** user password                        |

## System Info

| Command                                     | Purpose                                                             |
| ------------------------------------------- | ------------------------------------------------------------------- |
| `hostname`                                  | command may show valuable information about the role of the machine |
| `uname -a`                                  | show kernel info, are there any kernel vulnerabilites?              |
| `cat /proc/version`                         | may give info on kernel and if compiler is installed                |
| `cat /etc/issue` or<br>`cat /etc/*-release` | may give system info                                                |
| `arch`                                      | show architecture                                                   |

**Kernel Modules**

| Command                         | Purpose                                                            |
| ------------------------------- | ------------------------------------------------------------------ |
| `lsmod`                         | list loaded kernel modules<br>--> search for known vulnerabilities |
| `/sbin/modinfo <kernel_module>` | get further info about a kernel module                             |
| `ls /etc \| grep apparmor`      | check if apparmor is present (then it is likely also enabled)      |

## Processes & Services

**Note:** On linux, non privileged user can also list details of higher-privileged processes.

| Command                | Purpose                          |
| ---------------------- | -------------------------------- |
| `ps aux`               | show processes for all users     |
| `watch -n 1 "ps -aux"` | continuously watch all processes |

## Scheduled Tasks

configured cron-jobs are found in directories of format `/etc/cron.*`, e.g. `/etc/cron.hourly`, `/etc/cron.daily`

| Command                       | Purpose                                                       |
| ----------------------------- | ------------------------------------------------------------- |
| `ls -lah /etc/cron*`          | list all cron config files                                    |
| `cat /etc/crontab`            | show cronjobs configured in crontab - often these run as root |
| `crontab -l`                  | cronjobs configured for the current user                      |
| `grep "CRON" /var/log/syslog` | show cronjob logs                                             |

## Network

| Command                        | Purpose                                                                  |
| ------------------------------ | ------------------------------------------------------------------------ |
| `ifconfig` or<br>`ip a`        | info about network interfaces                                            |
| `netstat -anp` or<br>`ss -anp` | processes using the network - see [[3 Tools/utilities/netstat\|netstat]] |
| `route` or `routel`            | list routes                                                              |
| `ip route`                     | show which routes are associated with which interface                    |
| `cat /etc/iptables`            | might contain saved firewall rules                                       |
| `grep /etc/ "-A INPUT"`        | grep for iptables syntax to locate saved iptables rules                  |

## Installed Software

listing packages depends on the installed package manager.

| Command   | Purpose                                               |
| --------- | ----------------------------------------------------- |
| `dpkg -l` | list dpkg packages<br>default on debian-based distros |

## Search Files

Tool: [[3 Tools/utilities/find|find]] - use `2>/dev/null` to suppress error messages

| Command                     | Purpose                                                                                     |
| --------------------------- | ------------------------------------------------------------------------------------------- |
| `find / -type f -perm 0777` | find files with the 777 permissions (files readable, writable, and executable by all users) |
| `find / -perm a=x`          | find executable files                                                                       |

**writeable files/folders**

| Command                                                                                                                            | Purpose                              |
| ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| `find / -writable -type d 2>/dev/null` or<br>`find / -perm -222 -type d 2>/dev/null` or<br>`find / -perm -o w -type d 2>/dev/null` | Find writeable folders               |
| `find / -writable 2>/dev/null`                                                                                                     | search for writeable folders & files |
| `find / -perm -o x -type d 2>/dev/null`                                                                                            | find world-executabe folders         |

**time-based search

| Command            | Purpose                                               |
| ------------------ | ----------------------------------------------------- |
| `find / -mtime 10` | find files that were modified in the last 10 days     |
| `find / -atime 10` | find files that were accessed in the last 10 day      |
| `find / -cmin -60` | find files changed within the last hour (60 minutes)  |
| `find / -amin -60` | find files accesses within the last hour (60 minutes) |
| `find / -size 50M` | find files with a 50 MB size                          |

### Snippet: List user files

This snippet lists mount points, as well as all files in `/home/` and `/root/` 3 levels deep

```bash
echo -e "\n=== Drives & Mounts ==="; df -h --output=target | tail -n +2; echo -e "\n=== Home Directories ==="; find /home -maxdepth 3 2>/dev/null | while read f; do echo "  $f"; done; echo -e "\n=== Root Home ==="; find /root -maxdepth 3 2>/dev/null | while read f; do echo "  $f"; done; for dir in /media /mnt /opt /tmp; do echo -e "\n=== $dir ==="; find "$dir" -maxdepth 3 2>/dev/null | while read f; do echo "  $f"; done; done
```

## Mounts

| Command          | Purpose                                                                                             |
| ---------------- | --------------------------------------------------------------------------------------------------- |
| `cat /etc/fstab` | list drives mounted at boot time<br>**Note:** Also custom scripts might be in place to mount files. |
| `mount`          | list all mounted filesystems                                                                        |
| `lsblk`          | list all available disks - maybe not all are mounted?                                               |

# Hardening
