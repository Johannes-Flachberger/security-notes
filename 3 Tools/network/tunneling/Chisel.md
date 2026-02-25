---
tags:
  - "#type/tool"
Link: https://github.com/jpillora/chisel#usage
Purpose: encrypted http tunneling tool
---
# Info

encapulates datastreams in http + encrypts the data with ssh

opens a SOCKS proxy

client & server use the same binary

Binaries for multiple architectures can be found on [GitHub](https://github.com/jpillora/chisel/releases)

# Usage

**Start chisel server**

`chisel server --port <port> --reverse`

When a connection is received, the socks proxy listens on port 1080 per default.

**Start chisel client:**

`/tmp/chisel client 192.168.118.4:8080 R:socks`

| Option      | Purpose                                                 |
| ----------- | ------------------------------------------------------- |
| `--reverse` | connect to a server and start SOCKS proxy on the server |
| `R:socks`   | open reverse socks proxy connection                     |

> [!Hint] Force chisel to run in background
> use `> /dev/null 2>&1 &`

# Snippets
