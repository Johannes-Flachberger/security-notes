**Tags:** #type/tech-specific 

---
## XML
- extensible Markup language
- storing & transporting data
- platform & programming language independent
- human & machine readable

every document starts with xml prolog containing version and encoding
Documents consist of elements specified in <…> & </…>
elements have hierachy → root element and child elements

`<?xml version="1.0" encoding="UTF-8"?>`
`<mail>`
 `<to>falcon</to>`
 `<from>feast</from>`
 `<subject>About XXE</subject>`
 `<text>Teach about XXE</text>`
`</mail>`

XML can include system files with the system keyword
`<?xml version="1.0"?>`
`<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>`
`<root>&read;</root>`

## DTD - Document Type Definition
defines structure and the legal elemtents&attributes od an XML document
**Example:**
note.dtd - defenition of the document type
`<!DOCTYPE note [ <!ELEMENT note (to,from,heading,body)> <!ELEMENT to (#PCDATA)><!ELEMENT from (#PCDATA)> <!ELEMENT heading (#PCDATA)> <!ELEMENT body (#PCDATA)> ]>`
xml file that uses note.dtd
`<?xml version="1.0" encoding="UTF-8"?>`
`<!DOCTYPE note SYSTEM "note.dtd">`
`<note>`
 `<to>falcon</to>`
 `<from>feast</from>`
 `<heading>hacking</heading>`
 `<body>XXE attack</body>`
`</note>`
all the elements used are defined in the note.dtd file