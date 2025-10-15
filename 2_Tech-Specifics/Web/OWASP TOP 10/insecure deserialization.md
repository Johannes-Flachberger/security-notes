**Type:** #type/theory
**Tags:** #goal/exploitation 

---

No data sanitation is done when deserializing data.
**examples:**
- Classes/Objects can be serialized
- Cookies can be serialized and encoded. We can also serialize and encode a payload in a Cookie. When the website loads back the cookie eg. remote code can be executed. 
Vulnerabilites:
- serializable classes in CLASSPATH variable 
- use of insecure libraries
- API takes and deserializes data without prior filtering
### Impact
code execution by API
### Defense
- trust nobody - only deserialize data from trusted sources
- only deserialize primitive datatypes (no self-made classes)
- integrity check by digital signature before deserializing objects
- log deserialization errors