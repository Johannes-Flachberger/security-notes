---
tags:
  - "#type/tool"
  - "#attack/command-and-control"
  - "#attack/lateral-movement"
  - "#attack/defense-evasion"
Link:
Purpose: remote shells & tunneling
---
# Info

See [[2 Tech-Specifics/Network/Protocols/TCP 22 SSH|TCP 22 SSH]]

# Usage

`ssh [username]@[IP]`

| Option                                                     | Purpose                                                                                                                                        |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `-v`                                                       | to show more info (response headers,...)                                                                                                       |
| `-i`                                                       | specify private key file to use<br>required permissions on private key file:`600`<br>**Note:** ssh private keyfiles must end with a blank line |
| `-N`                                                       | dont send commands, only forwarded packets                                                                                                     |
| `-L [LOCAL_IP:]LOCAL_PORT:DEST_IP:DEST_PORT`               | local port forwarding<br>set `LOCAL_IP` to `0.0.0.0` to listen on all interfaces                                                               |
| `-D [LOCAL_IP:]LOCAL_PORT`                                 | dynamic port forwarding<br>set `LOCAL_IP` to `0.0.0.0` to listen on all interfaces                                                             |
| `-R <listening_ip>:<listening_port>:<dest_ip>:<dest_port>` | remote port forwarding                                                                                                                         |
| `-R [listening_ip]:<listening_port>`                       | dynamic remote port forwarding                                                                                                                 |

# Snippets

## SSH Tunneling

Further reading:

- [ssh.com](https://www.ssh.com/academy/ssh/tunneling-example)
- [iximiuz](https://iximiuz.com/en/posts/ssh-tunnels/)

> [!NOTE] Note
> Invoking ssh through a standard [[3 Tools/shells/Netcat|Netcat]] shell does not work. Try [[2 Tech-Specifics/OS/Linux/Reverse Shell Stabalisation|Reverse Shell Stabalisation Linux]] or [[2 Tech-Specifics/OS/Windows/Reverse Shell Stabilisation|Reverse Shell Stabilisation Windows]].

### Client --> Server

#### Local Port Forwarding

Packets are tunneled through ssh to the remote host and are then (by the remote host) forwarded to the specified destination host&port

**Command:**

```sh
ssh -N -L [local_ip]:<local_port>:<dest_ip>:<dest_port> <user>@<local_ip>
```

#### Dynamic Port Forwarding

Ssh sets up a local listening port as a SOCKS proxy. Packets are tunneled form the listening host to the remote host and then forwarded to a dynamic destination host.

**Command:**

```sh
ssh -N -D [local_ip]:<local_port> <user>@<local_ip>
```

**Important:** The client application using the tunnel must treat the ssh listening port as a SOCKS4 or SOCKS5 proxy. If an application does not support proxies use e.g. [[3 Tools/anonymity/proxychains|proxychains]].

### Server --> Client

Like a reverse shell for port forwarding.

**Workflow:**

1. start local ssh server: `sudo systemctl start ssh`
2. From the remote, connect back using ssh
3. Check if local port is listening: `ss -ntplu`

#### Remote Port Forwarding

> [!Hint] Usefull if inbound traffic is filtered on the target.

SSH connects back from a remote machine to the local machine and opens a listening port on the local machine. All packets sent to this listening ports are forwarded to the specified destination host & port.

**Command**:

```sh
ssh -N -R <listening_ip>:<listening_port>:<dest_ip>:<dest_port> <server_user>@<server_ip>
```

Most of the time, you want to set `<listening_ip>` to `127.0.0.1`

#### Remote Dynamic Port Forwarding

Similar to [[#Dynamic Port Forwarding]].

The ssh client connects to a server and opens a SOCKS proxy listening port on the server. Packets are tunneled from the server to the client and then forwarded to their destination host.

**Prerequisite:** SSH client version higher than 7.6 (ssh server version is irrelevant)

**Command:**

```sh
ssh -N -R [listening_ip]:<listening_port> <server_user>@<server_ip>
```

You can omit `[listening_ip]` to bind to localhost of the server.
