---
tags:
  - "#type/tool"
Link: https://github.com/sshuttle/sshuttle
Purpose: create vpn-like tunnel using ssh
---
# Info

Uses SSH to create a transparent proxy / VPN-like tunnel to a target system. All packets directed to the specified subnets are transmitted through the tunnel.

**Prerequities:**

- on SSH client: root privileges
- on SSH server: python3

# Usage

`sshuttle [-l [ip:]port] -r [user@]sshserver[:port] <subnets...>`

You can specify multiple subnets that shall be routed through the ssh tunnel.

Example: `sshuttle -r admin@192.168.x.x:2222 10.5.60.0/24`

# Snippets
