**Tags:** #type/tech-specific

---

execute shell commands on the webserver
-> you can try to steal information, open a reverse shell,...
two types: blind & verbose
# blind rce
- webapp does not output message
- use payloads that cause time delay and check if the website hangs for that amount of time eg. `ping` or `sleep`
- redirect output to eg. a file using `>` 
# verbose RCE
webapp gives output

# Useful payloads
https://github.com/payloadbox/command-injection-payload-list
https://hackersonlineclub.com/command-injection-cheatsheet/

## linux
- combine commands with `;`, `&` or `&&`
- `whoami`: show current user
- `ls`: show directory contents
- `ping`: application will hang for some time
- `sleep`: application will hang
- spawn reverse shell with netcat
## Windows
- `whoami`: show current user
- `dir`: show directory contents
- `ping`: application will hang for some time
- `timeout`: application will hang
# Filter Bypassing
- encode payload as hexadecimal

# Tipps & tricks
- with reverse shells, sometimes things dont work as expected, e.g. the nc -e option might not work. In this case try different commands/ variations fo the payload
# Remediation
**input sanitisation**

