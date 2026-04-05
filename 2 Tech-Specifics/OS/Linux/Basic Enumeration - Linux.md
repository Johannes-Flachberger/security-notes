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

## System Overview

### Users & Groups

| Command       | Purpose                                                                                        |
| ------------- | ---------------------------------------------------------------------------------------------- |
| `id [user]`   | show user & group info                                                                         |
| `/etc/passwd` | info on users, groups,... eg. grep for "home" to fin real users, not just service users        |
| `env`         | show all set environment variables<br>- eg PATH may contain useful compiler/scripting language |
| `sudo -l`     | list sudo privileges of current user<br>**Prerequisite:** user password                        |

### OS Info

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

### Network

| Command                        | Purpose                                                                  |
| ------------------------------ | ------------------------------------------------------------------------ |
| `ifconfig` or<br>`ip a`        | info about network interfaces                                            |
| `netstat -anp` or<br>`ss -anp` | processes using the network - see [[3 Tools/utilities/netstat\|netstat]] |
| `route` or `routel`            | list routes                                                              |
| `ip route`                     | show which routes are associated with which interface                    |
| `cat /etc/iptables`            | might contain saved firewall rules                                       |
| `grep /etc/ "-A INPUT"`        | grep for iptables syntax to locate saved iptables rules                  |

# Hardening
