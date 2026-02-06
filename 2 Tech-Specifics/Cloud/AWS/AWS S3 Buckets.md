---
tags:
  - "#type/tech-specific"
---
# Fundamentals

**See:**
- [Access Methods](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-bucket-intro.html)

# Pentesting

# Enumeration

- List bucket contents (if allowed)
	- browse the bucket root
	- e.g. `http://domain/bucket_name`
- analyse the bucket name to discern other bucket names
	- often bucket names follow a naming convention
	- often bucket names include a short random part, since they must be unique accross a region - maybe organisations share the same random part accross all their buckets?

# Hardening
