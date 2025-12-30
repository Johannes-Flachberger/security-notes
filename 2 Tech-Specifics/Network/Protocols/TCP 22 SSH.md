---
tags:
  - "#type/tech-specific"
  - attack/command-and-control
---
# Fundamentals
-  used for: server access, data transfer, channeling of other protocols
- port 22
# Pentesting
## Command and control
## SSH Usage
`ssh [username]@[IP]`

| Option | Purpose                                                                                                                                        |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `-v`   | to show more info (response headers,...)                                                                                                       |
| `-i`   | specify private key file to use<br>required permissions on private key file:`600`<br>**Note:** ssh private keyfiles must end with a blank line |

**security features:**
1. You can confirm the identity of the remote server
2. Exchanged messages are encrypted and can only be decrypted by the intended recipient
3. Both sides can detect any modification in the messages
4. credentials are sent encrypted