---
tags:
  - "#type/tech-specific"
---
# /etc/passwd

Line format:

`<username>:<password>:<UID>:<GID>:<comment>:<home_directory>:<login_shell>`

- if `password` is `x`: password hash in /etc/shadow file
	- **Note:** If a password hash is set in `etc/passwd`, it overrides `/etc/shadow`
- `<comment>`: additional info about user
- normal user `<UID>` starts from 1000

# Security Measures

## AppArmor

A [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control)system for linux. It runs in parallel to usual permission, capabilities, etc. and sets constraints what an application is allowed to do. Each application has its own profile in `/etc/apparmor.d/`. See https://apparmor.net/

| Command                                | Purpose                                      |
| -------------------------------------- | -------------------------------------------- |
| `aa-status`                            | check if AppArmor is enabled (requires root) |
| `cat /var/log/syslog \| grep apparmor` | check logs                                   |
