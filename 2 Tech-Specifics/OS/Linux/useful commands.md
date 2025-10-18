**Tags:** #type/tech-specific 

---

`fuser -m -v [path]`: find processes that use the specified file/folder

grant sudo without password for current user
`echo $USER"  ALL=(ALL:ALL) ALL" > $USER"_sudo_nopasswd"`
`sudo mv $USER"_sudo_nopasswd" /etc/sudoers.d

# Funny permissions trick
What if we cannot use chmod to change the permissions on a file?
copy a file with the necessary permissions set using cp
Then only grap the contents of a file and put them in the copied file using `cat file_with_content > file_with_permissions´