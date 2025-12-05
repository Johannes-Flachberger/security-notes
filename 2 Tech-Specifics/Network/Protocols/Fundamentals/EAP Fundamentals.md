**Tags:** #type/tech-specific

---
standard framework for authentication on networks
often used with 802.1x
NAC = Network access control

## FAST
EAP flexible authentication via secure tunneling
mutual authenticaiton + TLS tunnel
comon with RADIUS

## PEAP
also TLS, no PSK but certificate
MSCHAPv2 is a variant of this made by microsoft 

## EAP-TLS
mutual authentication via certificates
quite complex because PKI is needed

## EAP-TTLS
tunneled TLS 
can tunnel other authentication protocols
cert on the authentication server build TLS tunnel using certificate, then tunneling is in place
