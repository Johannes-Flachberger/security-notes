tags: #type/theory #goal/exploitation

---

- read, or even write to file locations you should not have access to
- commonly, if a webserver can display files
- possible if poor input sanitazion is applied
- Most of the time the webserver runs as dedicated user that has restricted permissions - but it is still worth trying.
- Interesting files for directory traversal: [[2_Tech-Specifics/OS/Sensitive Files|Sensitive Files]]
	- e.g. on Linux: find users -> check their ssh keys -> possibly log in using ssh
# Entry Points:
- links that take a file as parameter
# Sub-Techniques
## Path traversal
- eg. if in PHP the `file_get_contents` function is used
- posssible if poor input filtering is applied

**Tips & Tricks**
- You can add as many `../`sequences as you want - once the filesystem root is reached, the access `../` sequences are "ignored"
- On linux use `../`, on windows `..\` 
- When using [[3_Tools/web/cURL|cURL]] : use the `--path-as-is` option
- append `/.` to the path to circumvent eg. extension filters
- apply URL [[2_Tech-Specifics/Web/Fundamentals/encodings|encoding]] to circumvent weak input sanitation 
	- It an also help to only encode certain characters, e.g. `.` as `%2e` 
## Local File Inclusion (LFI)
- exploits the include function (used eg. for language switches)
- error messages help a lot to figure out how the webserver is accessing the files
## Remote File Inclusion (RFI)
- option `allow_url_fopen` on the webserver needs to be set
