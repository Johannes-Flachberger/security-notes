**Tags:** #type/tech-specific #tactic/credential-access #tactic/exfiltration #tactic/discovery 

---
# Fundamentals
- read files the webserver should not have access to
- commonly, if a webserver can display files
- possible if poor input sanitazion is applied
## Entry Points:
- links that take a file as parameter
- eg. if in PHP the `file_get_contents` function is used
# Pentesting
Most of the time the webserver runs as dedicated user that has restricted permissions - but it is still worth trying.
- Interesting files for directory traversal: [[2 Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
	- e.g. on Linux: find users -> check their ssh keys -> possibly log in using ssh
- You can add as many `../`sequences as you want - once the filesystem root is reached, the access `../` sequences are "ignored"
- On linux use `../`, on windows `..\` 
- dont mix relative and absolute paths - e.g. `..\..\C:logs\example.log` would not work.
- When using [[3 Tools/web/cURL|cURL]] : use the `--path-as-is` option
- append `/.` to the path to circumvent eg. extension filters
**Filter Bypassing**
[[2 Tech-Specifics/Web/WebApp Attacks/Attacks/Injection Attacks/Filter Bypassing|Filter Bypassing]]
# Hardening
sanitize input for `../` sequences and their encoded variants
