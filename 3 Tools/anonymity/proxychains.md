---
tags:
  - "#type/tool"
  - "#defend/harden"
Purpose: route traffic of a command through one or multiple proxies
Link: https://github.com/rofl0r/proxychains-ng
---
# Info

route traffic of a command through one or multiple

# Usage

put `proxychains` in front of command you want to use

E.g.: `proxychains nmap -sS ...`

## Configuration

The proxy addresses, port & mode must be set in the config file at `/etc/proxychains4.conf`

**Note:** http proxies are faster than socks proxies

## Port-scanning over proxychains

- The values `tcp_read_time_out` and `tcp_connect_time_out` specify the timeouts proxychains uses. By default, they are very high --> reduce to speed up port scans.
- Must be run with root privileges.
- skip icmp discovery

```bash
sudo proxychains nmap -Pn -sT ...
```

# Snippets
