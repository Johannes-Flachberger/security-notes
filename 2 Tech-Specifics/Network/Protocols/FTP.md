---
tags:
  - "#type/tech-specific"
  - "#attack/initial-access/server-side"
---
# Fundamentals

FTP - File Transfer Protocol

**Default Ports:**

- tcp20: data
- tcp21: control

operates on 2 channels/ports: control channel for commands & data channel for data

- very efficient
- credentials and commands are sent in cleartext!

### 2 Modes:

1. **active:** data is sent over a separate channel originating from the FTP server’s port 20
2. **passive:** data is sent over a separate channel originating from an FTP client’s port above port number 1023

## Usage

`ftp <user>@<ip>`

| Option | Purpose         |
| ------ | --------------- |
| `-A`   | use active mode |

**In FTP shell:**

| Command            | Purpose                      |
| ------------------ | ---------------------------- |
| `STAT`             | show some info               |
| `SYST`             | show sytem type              |
| `TYPE A`           | use ASCII for file transfer  |
| `TYPE I`           | use binary for file transfer |
| `ls`               | list files                   |
| `less`             | show start of file contents  |
| `get <filename> -` | show file content            |
| `put <path>`       | send file                    |

# Pentesting

## Password Attacks

Check for anonymous login:

- Username: `anonymous`
- Password: `anonymous` or nothing
