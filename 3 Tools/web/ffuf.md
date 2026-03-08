---
tags:
  - "#type/tool"
Link: https://www.kali.org/tools/ffuf/
Purpose: directory discovery, vhost discovery and HTTP parameter fuzzing
---
# Info

fuzzing tool, e.g. used for [[2 Tech-Specifics/Web/WebApp Attacks/Injection Attacks/SQL Injection|SQL Injection]], directory discovery, vhost discovery, etc.

# Usage

First make a valid request and note the response size, then use that as `<baseline_size>`

`FUZZ` key word will be replaced by the parametes in the wordlist

**Example:**

```sh
ffuf -u "http://target.com/page?id=FUZZ" \
     -w /usr/share/seclists/Fuzzing/SQLi/Generic-SQLi.txt \
     -mc 200,500 \
     -fs <baseline_size>
```

# Snippets
