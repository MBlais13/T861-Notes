#protocols 

Prevents loops within the network


During STP functions, switches use Bridge Protocol Data Units (BPDUs) to share information about themselves and their connections. BPDUs are used to elect the root bridge, root ports, designated ports, and alternate ports.



STP compensates for a failure in a network by recalculating and opening up previously blocked ports.


# Portfast
Portfast is **a Cisco technique that puts a switch interface into forwarding mode immediately, skipping the listening and learning states**. This is useful for interfaces that connect to computers or servers so that these devices don't have to wait until the interface is up and running.