**Tags:** #type/note #todo 

---
# WLAN basics
WLAN operates on OSI L2, just as ethernet does - therefore Ethernet (LAN) and WLAN can interoperate on one Network. However, for this an access point is necessary. Routers are only necessary for inter-network communication (L3).
If there are multiple access points in a network, you usually use a RADIUS (Remote Authentication Dial-in User Service) or server to handle authentication to the network. Another option is to configure the same authentication data on all the access points.

>[!note] Home Wifi-Routers are most of the time a combination of Router, WLAN Access Point, and Switch.

# IEEE 802.1X
Also called network access control (NAC) or port-based network access control (PNAC).
the goal is to enforce authentication on the network - if a client connect to a physical (ethernet) port, WLAN or VLAN, authentication is required before a connection to the network is permitted.
uses [[2 Tech-Specifics/Network/Protocols/RADIUS|RADIUS]] and [[2 Tech-Specifics/Network/Protocols/EAP - Extensible authentication protocol|EAP]] (Extensible Authentication Protocol)

3 main components:
Supplicant: client, that knows IEEE 802.1X
Authenticator: Supplicant talks to Authenticator directly
Authentication server: Authenticator checks credentials with authentication server

## How is the access control implemented?
All switch ports are disabled by default. - Authentication attempts are still possible. If a successfull authentication is done, the switch is reconfigured and the (phyiscal) port the client is connected to is enabled (and often assigned a certain VLAN). The client can then communicate on the network. 