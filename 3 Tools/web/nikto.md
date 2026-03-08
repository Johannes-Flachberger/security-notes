---
tags:
  - "#type/tool"
Link: https://www.kali.org/tools/nikto/
Purpose: quick webapp vulnerability scanner, focus on server misconfigurations
---
# Info

Nikto is a web server scanner that checks for misconfigurations, outdated software, and dangerous files/headers.

Comparison to [[3 Tools/web/OWASP ZAP|OWASP ZAP]]: Nikto is quicker, less thorough, but its speciality are server misconfigurations - here it is better than ZAP.

# Usage

**Example:** `nikto -h http://target.com`

| Option    | Purpose                        |
| --------- | ------------------------------ |
| `-h`      | Target host or IP              |
| `-p`      | Port (default 80)              |
| `-ssl`    | Force SSL/HTTPS scan           |
| `-o`      | Output to file                 |
| `-Format` | Output format (txt, html, csv) |

# Snippets

```bash
# Basic scan
nikto -h http://target.com

# HTTPS target
nikto -h https://target.com -ssl

# Specific port
nikto -h http://target.com -p 8080

# Save output
nikto -h http://target.com -o results.html -Format html
```
