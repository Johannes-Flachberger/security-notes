**Tags:** #type/tool #defend/harden
**Purpose:** route traffic of a command through a chain of proxies

---
# Info
route traffic of a command through a chain of proxies
# Usage
config file in `/etc/proxychains4.conf`

put `proxychains` in front of command you want to use, eg `proxychains nmap -sS ....`
configure proxylist, mode,... in config file
google online for free proxy servers

to check if it works
eg. `proxychains firefox google.com`

> [!tip] http proxies are faster than socks
## tor service
`service tor stert/restart/status/stop`

