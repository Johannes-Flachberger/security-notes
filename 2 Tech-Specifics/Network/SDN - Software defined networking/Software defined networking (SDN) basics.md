**Tags:** #type/note 

---
Switches and routers are not configured individually and decide what to do based on high level rules. Instead, each switch and router is connected to a controller that decides what to do with each packet. This controller instructs the switches (and routers?) what to do with the packet using the [[2 Tech-Specifics/Network/SDN - Software defined networking/Openflow|Openflow]] protocol. Each switch has a flowtable that contains the rules to match each packet against - these rules are created on the fly by the controller. 