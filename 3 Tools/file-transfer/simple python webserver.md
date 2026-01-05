---
tags:
  - "#type/tool"
  - "#attack/exfiltration"
Link:
Purpose: serve files using http
---
# Info

sets up a 3 python webserver, then you can access files from remote machines that you are reachable from

more advanced alternatives:

- [[3 Tools/file-transfer/updog|updog]]
- [[3 Tools/file-transfer/raven|raven]]

# Usage

execute in directory to make files accessable via [[2 Tech-Specifics/Network/Protocols/TCP 80, 443 HTTP(S)|HTTP]] requests

`python3 -m http.server [port]`
