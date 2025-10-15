tags: #type/theory #tech/web #goal/exploitation

---

## Upload filtering
various methods exist for file upload filtering:
### Extension filtering
looks at the file extension
extensions can be easily faked
### File type filtering
**MIME filtering**
Multipurpose Internet Mail Extension types are used in the web to identify file types.
MIME is based on file extension -> easy to bypass
**Magic number validation**
magic number =  a binary number at the beginning of every file that tells the file type
might be faked, but is a little harder than extensions
### Length filtering
typically not a problem for uploading shells
### Name filtering
very usual, simple name sanitation
usually, files are renamed on upload
### Content filtering
not done very often
## Bypass client side filtering
client side filtering often is done by javascript in your browser
a basic ways to bypass
1. turn off javascript in the browser
2. intercept and modify the incoming page - eg with burp
3. interceot and modify the file upload - eg with burp
4. send file directly to upload point -  eg with curl
## Bypass server side filtering
there are different kinds of server side filters, eg:
1. file extension filters
2. magic number filters
magic numbers of different file types:
https://en.wikipedia.org/wiki/List_of_file_signatures
use hexeditor to edit hex of a file and change magic number