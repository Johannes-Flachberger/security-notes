**Tags:** #type/tool
**Link:** https://www.geeksforgeeks.org/linux-unix/wget-command-in-linux-unix/ 
**Purpose:** Download files using http(s)

---
# Info
Download files using http(s)
# Usage  
`wget [options] [URL]`

- `-E`: Adjust file extensions to match MIME type
- `-k`: Convert links in downloaded pages to local links
- `-K`: Keep original files (save as `.orig`)
- `-p`: Download all files needed to display the page properly
- `-e robots=off`: Ignore `robots.txt`
- `-H`: Allow downloads from other hosts
- `-D<domain>: Restrict external downloading to the specified domain`
- `-nd`: Save all files in a flat directory (no folders)
# Snippets
###### Copy a webpage with all its files
``` bash
wget -E -k -K -p -e robots=off -H -Dexample.com -nd "https://example.com/signin"
```

