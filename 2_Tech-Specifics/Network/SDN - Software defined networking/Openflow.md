tags: #type/note #tech/protocol #tech/network/sdn

---
Protocol used for software defined networking.
The controller and switch talk to each other using openflow.
If the switch receives a packet that does not match an entry in a flow table, it sends an openflow packet to the controller to ask what to do with it. The controller then answers with an action, or an adaption of the flow table.