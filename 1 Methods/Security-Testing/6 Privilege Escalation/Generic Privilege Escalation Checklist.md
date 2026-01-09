---
tags:
  - "#type/method"
  - "#attack/privilege-escalation"
---

---

Generic privilege escalation checklist:

- [ ] Username and hostname
- [ ] Group memberships of the current user
- [ ] Existing users and groups
- [ ] Operating system, version and architecture
- [ ] Network information
	- [ ] Routes
	- [ ] DHCP status
	- [ ] local services using the network
	- [ ] network interfaces of hypervisors/container engines
- [ ] Installed applications & their versions
- [ ] Running processes
	- [ ] processes running as privileges user
- [ ] Scheduled Tasks
