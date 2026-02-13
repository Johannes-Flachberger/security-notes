---
tags:
  - "#type/tech-specific"
  - "#attack/discovery"
  - "#attack/collection"
---
# Fundamentals

Most container engines use Linux kernel features under the hood - therefore the umbrella term "Linux Containers". This includes Docker, Podman, LXC/LXD etc.

# Pentesting

## Enumeration

As Linux containers basically are Linux, the enumeration techniques described in [[2 Tech-Specifics/OS/Linux/Privilege Escalation Linux/Overview - Privilege Escalation Linux|Privilege Escalation Linux]] form the basis for enumeration. Here, only some specifics are listed.

### Check Mounts

Permanent data, such as configs and secrets are often mounted into the container - check with `cat /proc/mounts`. **Note:** Usually, already lots of mounts are present to make the container work - look for anything standing out.

### Check Privileged Mode

Containers can run in privileged mode, granting them lots of permissions ("capabilities") on the host.

**Note:** In order to use these capabilities for container breakout, you need root privileges within the container first.

**Workflow:**
1. Check values of values in `CapPrm`, `CapEff`, and `CapBnd`: `cat /proc/1/status | grep Cap`
2. On kali, decode the Capability values using `capsh`: e.g. `capsh --decode=0000003fffffffff`
3. look for the capabilities `cap_net_admin` and `cap_sys_admin`

# Hardening
