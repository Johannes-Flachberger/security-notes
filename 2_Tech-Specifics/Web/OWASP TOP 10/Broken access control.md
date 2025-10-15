**Type:** #type/theory
**Tags:** #goal/exploitation 

---

a great variety of vulnerabilities is possible
attackers can bypass authorization and view sites they should not be able to view
e.g. https://example.com/blog_posts?file=../../../../etc/passwd
e.g. https://example.domain/admin

- access is possible by directly entering the URL of the resource
- hidden form fields which bypass access control
- metadata (cookies, jwt,...) can be manipulated
- errors in access control fields
### Impact
- evelated priviledge for attackers
- lateral movement
### Defense
- implement access control centrally on server, nothing on the clients
- correct config is essential
- no access per default - whitelist privileged users
- classify data & functionality clearly
- protect metadata from manipulation
- log access control violations
## Eg. IDOR - Insecure Direct Object Reference
eg. which account we log into is encoded in the url, so we can simply change what it says in the url
For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like this [https://example.com/bank?account_number=1234](https://example.com/bank?account_number=1234). 

There is however a potentially huge problem here, a hacker may be able to change the account_number parameter to something else like 1235 to access another account