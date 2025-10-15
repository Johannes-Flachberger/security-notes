tags: #type/theory

---
great tool for encoding/decoding: [[3_Tools/defensive/Cyberchef|Cyberchef]]
# base64
binary encoding the characters, "=" is a placeholder
eg. `TGV0J3MgU3RhcnQgU2ltcGxl`
often ends with `==`
# URL
some characters are exchanged for their hexadecimal preceded with %
eg. `%4e%65%78%74%3a%20%44%65%63%6f%64%69%6e%67`
# HTML
special characters are replaced by & followed by hexadecimal or a keyword, eg  `&quot` for `"` eg. `&#x25;&#x33;&#x34;&#x25;&#x33;&#x37;`
# Gzip
compression technique used for web-technologies