kalitags: #type/note

---
# DVWA - Damn vulnerable web application
## brute force
brute force with burp cluster bomb
## command execution
end ping command with ; | or && and then enter another command
## CSRF - cross site request forgery
1. get request in burp
2. write proof of concept script
```html
<html>
	<head>
		<title>CSRF Proof of Concept</title>
	</head>
	<body>
		<h1>CSRF Example</h1>
		<img style="display:none" src="ENTER THE FORGED REQUEST HERE" alt="">
	</body>
</html>
```

usually you do a 1:1 copy of the webpage and insert this snippet with a hidden image
3. in the hidden image src part you enter the request you want to be sent
4. you present the malicous wite to some user the request will be sent using his session ID -> you might be able to change credentials, retrieve information,...
## Insecure captcha
doesnt work anymore
## File Inclusion
change page parameter in request to some file like /etc/passwd
can you include a remote file?
## SQL injection
[[2 Tech-Specifics/Web/Web Application Attacks/SQL Injection]]
## upload vulns
upload a simple php webshell
```php
<?php
	system($GET["cmd"]);
?>
```

then send request to this file on the webserver and pass a command in cmd parameter
## XSS
enter a script tag
```html
<script>alert();</script>
```

```html
<script>alert(document.cookie);</script>
```

# OWASP mutillidae

just explore and hackk :)
# bWAPP
better use on 10.0.1.11 
## HTML Injection
insert script tag for cross site scripting

## XPAth injection (logon)
Xpath is the query languag used for databases which use xml as file format
`' or '1'='1 ` dont forget the space at the end!
## XPath Injection (search)
irgendwie kompliziert
## PHP injection
in URL parameter message ändern zu php info oder so
## man in the middle
sniff credentials with wireshark

