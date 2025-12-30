---
tags:
  - "#type/tool"
Link: 
Purpose: find files on linux
---
# Info

# Usage

`find <directory> [arguments]`

e.g. `find / -type f -name "myfile*"

| Argument      | Purpose                                                             |
| ------------- | ------------------------------------------------------------------- |
| `2>/dev/null` | Suppress error and permission messages                              |
| `-type`       | Filter by type (e.g., `f` = file, `d` = directory)                  |
| `-perm`       | Match permission bits (e.g., `0777`, `a=x`, `-222`, `-o w`, `-o x`) |
| `-writable`   | Items writable by the current user                                  |
| `-user`       | Match items owned by a specific user                                |
| `-mtime`      | Match files based on modification time in days                      |
| `-atime`      | Match files based on last access time in days                       |
| `-cmin`       | Match files based on metadata change time in minutes                |
| `-amin`       | Match files based on access time in minutes                         |
| `-size`       | Match files by size (e.g., `50M`)                                   |
| `-name`       | Case-sensitive filename pattern                                     |
| `-iname`      | Case-insensitive filename pattern                                   |
| `-exec`       | Execute a command for matched items (`{} \;` or `{}` +)             |
| `-maxdepth`   | Limit search to a maximum directory depth                           |
| `-mindepth`   | Ignore results above a minimum directory depth                      |
| `-path`       | Match based on full path pattern                                    |
| `-prune`      | Exclude directories from the search                                 |
| `-printf`     | Custom output formatting (GNU find only)                            |

# Snippets
