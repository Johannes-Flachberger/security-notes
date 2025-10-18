**Tags:** #type/tech-specific

---
# Overview
Injection attack - vulnerable when website uses unsanitized user input and interprets it as code.
A payload is injected and executed by a users browser. --> the payload always runs in the users context - e.g. if an admin user runs the payload, privilege escalation is performed

**General entry points**
- Whenever data is entered to the website
## Possible Impacts
- Session Hijacking: Stealing session cookies, stealing session nonces
- Forced redirection to another malicious page
- command injection
- manipulate DOM
## Defense
- all data loaded by a website must be HTML encoded
- validate/sanitize all data from non-trusted sources - user, APIs, backend servers
- use webframeworks - those use HTML encoding by default
## Example: Vulnerable Webpage
``` php
<html>
	<h1>Suchergebnisse</h1>
	<p><?php echo $userInput; ?> </p>
</html>
```
# Theory
## Stored XSS
Malicious Payload is injected and stored in a cache or database of the webserver - then when the payload is retrieved, it is executed in a site users browser.
**Example:** a blog website: the payload is written in a comment field -> everybody who loads that comment loads the payload

Points of entry:
- In general: Whenever data is entered and viewed later by users
- Comments on a blog
- product reviews
- User profile information 
- Website Listings
## Blind XSS
- similar to stored XSS
- you do not see directly if the payload works -> put a callback in the payload (eg. HTTP request)
## Reflected XSS
Payload is inserted n the HTTP request to the website, eg some input to a search field. The request with the XSS is sent to the webserver and then sent back (reflected) to you. - only affects persion that visits the link/submits the request

Points of entry:
-  Parameters in the URL Query String
-  URL File Path
-  Sometimes HTTP Headers (although unlikely exploitable in practice)
## DOM-based XSS (Document Object Model)
vulnerability is in the client side code.
DOM is a programming interface for HTML and XML documents. It represents the page (i.e. stays in sync with the HTML code) so that programs can change the document structure, style and content. - e.g. every time you use `document.` in javascript you access the DOM. --> since javascript can manipulate the DOM, XSS can manipulate the DOM.

Points of entry:
1. look for parts of the code in javascript that access certain variables that an attacker can have control over, such as `window.location.x` parameters
2. check if those variables are written to the Dom or handled by unsafe javascript functions

