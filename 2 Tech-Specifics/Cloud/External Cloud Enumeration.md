---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance"
---
# Fundamentals

When performing reconnaissance on cloud systems, the starting point is usally the domain name.

## Checklist:

Cloud Services intended for public accessibility typically use specific base domain names:

| AWS              | Azure                 | GCP                    |
| ---------------- | --------------------- | ---------------------- |
| s3.amazonaws.com | web.core.windows.net  | appspot.com            |
| awsapps.com      | file.core.windows.net | storage.googleapis.com |
|                  | blob.core.windows.net |                        |
|                  | azurewebsites.net     |                        |
|                  | cloudapp.net          |                        |

# Pentesting

**Workflow:**

1. [[#Enumerate public cloud ressources|Find publicly accessible cloud resources]] of the target  
2. [[#Enumerate resources for attack vectors]]

## Enumerate public cloud resources

### Generic Enumeration Techniques

These generic enumeration techniques are relevant for cloud services.

**Checklist:**

- [ ] Perform [[1 Methods/Security-Testing/1 Reconnaissance/Passive Recon/Overview - Passive Recon|Generic Passive Recon]]
- [ ] Perform [[2 Tech-Specifics/Network/Protocols/TCP,UDP 53 DNS#Enumeration|DNS Enumeration]] and [[2 Tech-Specifics/Web/WebApp Enumeration/Subdomain Enumeration|Subdomain Enumeration]]
	- [ ] perform reverse lookups of discovered IPs to identify the service-specific domain name
		- this most often reveals the type of the used AWS resource
- [ ] For web-pages: [[2 Tech-Specifics/Web/WebApp Enumeration/Overview - WebApp Enumeration#Debugging Page Content|Overview - WebApp Enumeration]]
	- [ ] Cloud-hosted webpages often load ressources from another cloud service, e.g. Amazon S3 - this helps to identify other cloud services in use

### Automated Enumeration

**Tools:**
- [[3 Tools/cloud/cloud-enum|cloud-enum]]
- [cloudbrute](https://www.kali.org/tools/cloudbrute/)

### Service specific techniques

**See:**
- [[2 Tech-Specifics/Cloud/AWS/AWS Enumeration#Find public cloud ressources|AWS Enumeration]]

## Enumerate resources for attack vectors

**See:**
- [[2 Tech-Specifics/Cloud/AWS/AWS Enumeration|AWS Enumeration]]

### Condition Based Enumeration

Often, properties such as account IDs can be enumerated based on specifically crafted conditions that, e.g. matches on a specific digit within the account ID. The concrete implementation depends on the context. For example see [[2 Tech-Specifics/Cloud/AWS/AWS S3 Buckets#Enumerate Account ID|AWS S3 Bucket Account ID Enumeration]]

# Hardening
