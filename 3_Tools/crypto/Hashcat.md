**Type:** #type/tool
**Tags:**  #goal/cracking
**Link:** https://hashcat.net/hashcat/
**Purpose:** hashcracking

---
# Info
> [!warning] may not work in VMs

find hash mode numbers on: [https://hashcat.net/wiki/doku.php?id=example_hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)
# Usage
put hashes to be cracked in file → run hashcat → cracked hashes are in potfile or in output file
`./hashcat.exe -m [hash mode number] -a [attack mode] ./[hash file] ./[wordlist file]`
`optional options: -o [output file] -O (optimized kernel, limits password length to 27 chars)`
