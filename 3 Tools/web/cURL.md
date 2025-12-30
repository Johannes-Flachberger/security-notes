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

| Argument           | Purpose                                                                                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-X <VERB>`        | set request type (verb) eg. `POST`,`GET`                                                                                                                           |
| `-H <key: value>`  | set HTTP header - e.g. `-H 'Content-Type: application/json'`                                                                                                       |
| `--data <data>`    | set data                                                                                                                                                           |
| `--data-urlencode` | specify url-encoded data - e.g. `--data-urlencode "cmd=which nc"`                                                                                                  |
| `-c <path>`        | store received cookies in file                                                                                                                                     |
| `-b <path>`        | send cookies in file                                                                                                                                               |
| `-i`               | show respnse headers in output                                                                                                                                     |
| `--path-as-is`     | usually, curl follows RFC 3986 rules for URI path normalization (removing `/../` and `/./` segments) - with this option, paths are interpreted exactly as supplied |
