---
tags:
  - type/tool 
  - attack/reconnaissance/passive 
Link: https://www.google.com/advanced_search
Purpose: advanced online search
---
# Info
use advanced search featrues to find content

**Ressources:**
- [google search operator reference](https://www.googleguide.com/advanced_operators_reference.html)
- [Google hacking database](https://www.exploit-db.com/google-hacking-database): collection of great queries
- [Google dork builder](https://dorksearch.com/)
# Usage
**Workflow:** start broad, then get narrow with operators
## `-`
exclude matching items from search
e.g. `-site:google.com`
## `site`
limits searches to the given domain
e.g. `site:google.com`
## `filetype`
limits search results to specified file type
can be useful to find programming language of the website
## `cache`
view cached version of the web page.
e.g. `cache:www.eccouncil.org`
## `inurl`
restricts the results to pages containing the word specified in the URL `inurl: copy site:www.eccouncil.org`
see also: allinurl
## `intitle`
restricts results to pages containing the query term in the title
e.g. `intitle:"index of"` to find directory listing pages
## `link`
searches websites or pages that contain links to the specified website or page
## `related`
displays websites that are similar or related to the URL
## `location`
This operator finds information for a specific location.
# Snippets

```css
filetype:php
filetype:asp     
old technology – Late 90s
filetype:asp intitle: admin login
inurl:admin.php
Allinurl: aspx php
filetype:asp inurl:php
inurl:intranet intitle:human resources
filetype:asp inurl:hr inurl:intranet
```
