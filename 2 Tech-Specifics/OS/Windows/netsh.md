---
tags:
  - "#type/tech-specific"
  - "#attack/lateral-movement"
---
# Fundamentals

Built-in command line firewall config tool.

See: [netsh docs](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/netsh)

**Prerequisites:**
- local admin privileges

Commands are categorized into:

- contexts - e.g. ipsec, firewall, portproxy
- sub-contexts: option of each context

# Pentesting

## Configure Proxies

**Show proxies:**

```cmd
netsh interface portproxy show all
```

**Add portforward:**

```cmd
netsh interface portproxy add v4tov4 listenport=<listen_port> listenaddress=<listen_ip> connectport=<destination_port> connectaddress=<destination_ip>
```

Check success with: `netstat -anp TCP | find "<listen_port>"`

**Remove portforward**

```
netsh interface portproxy del v4tov4 listenport=<listen_port> listenaddress=<listen_ip>
```

## Configure Firewall

**Add Rule:**

Example:

```
netsh advfirewall firewall add rule name="port_forward_ssh" protocol=TCP dir=in localip=192.168.50.64 localport=22 action=allow
```

**Delete Rule:**

Example:

```
netsh advfirewall firewall delete rule name="port_forward_ssh"
```

# Hardening
