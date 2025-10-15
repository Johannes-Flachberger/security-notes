**Type:** #type/tool
**Tags:**  
**Link:** https://www.googleguide.com/advanced_operators_reference.html
**Purpose:** Reconnaissance using Google

---
# Approach
use google or any other search engine features to find content
start broad, then get narrow with operators
# Ressources
**Google hacking database** - collection of great queries
https://www.exploit-db.com/google-hacking-database
**Google dork builder**
https://dorksearch.com/
**operator reference**
https://www.googleguide.com/advanced_operators_reference.html
**advanced search gui**
https://www.google.com/advanced_search
# Essential operators
## `-
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
restricts results to pages containing  the query term in the title
e.g. `intitle:"index of"` to find directory listing pages
## `link`
searches websites or pages that contain links to the specified website or page
## `related`
displays websites that are similar or related to the URL
## `location`
This operator finds information for a specific location.
# example queries
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
´´´
