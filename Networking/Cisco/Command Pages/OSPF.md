#cisco #load-balancing

> [!info] Commands
> [[Cisco Commands#OSPF]]

OSPF is a link-state routing protocol.

- OSPF can do MD5 authentication.
- OSPF can do clear text authentication.
- You can enable authentication for the entire area or a single interface.

- IOS(15) supports a maximum of 32 paths for OSPF

---
## Problem and solution
OSPF works differently than RIP or EIGRP, first of all, it’s a link-state compared to a distance vector (RIP), but it also doesn’t just send the link-state advertisements around. Routers have to become neighbors first. Once we have become neighbors, we are going to exchange link-state advertisements.  

- **Link**: That’s the interface of our router.
- **State**: Description of the interface and how it’s connected to neighbour routers.

![OSPF Designated Router](https://cdn.networklessons.com/wp-content/uploads/2013/02/ospf-designated-router.png)

OSPF works with the concepts of **areas,** and by default, you will always have a single area, normally, this is area 0 or also called the **backbone** area.

![OSPF Multi Area](https://cdn.networklessons.com/wp-content/uploads/2013/02/ospf-multi-area.png)

- Routers in the backbone area (area 0) are called backbone routers.
- Routers between 2 areas (like the one between area 0 and area 1) are called **area border routers** or **ABR.**
- Routers that run OSPF and are connected to another network that runs another routing protocol (for example, RIP) are called **autonomous system border routers** or **ASBR.**

### Hello packet
![OSPF Hello Packet Attributes](https://cdn.networklessons.com/wp-content/uploads/2013/02/ospf-hello-packet-attributes.png)

Many fields in the hello packet have to match otherwise they wont become neighbours.
- **Router ID:** Each OSPF router needs to have a unique ID which is the highest IP address on any active interface. More about this later.
- **Hello / Dead Interval:** Every X seconds, we will send a hello packet. If we don’t hear any hello packets from our network for X seconds, we declare you “dead,” and we are no longer neighbors. These values have to match on both sides to become neighbors.
- **Neighbors:** All other routers who are your neighbors are specified in the hello packet.
- **Area ID**: This is the area you are in. This value has to match on both sides to become neighbors.
- **Router Priority:** This value is used to determine who will become designated or backup designated routers.
- DR and BDR IP address: Designated and Backup Designated router.
- **Authentication password:** You can use clear text and MD5 authentication for OSPF, meaning every packet will be authenticated. Obviously, you need the same password on both routers in order to make things work.
- **Stub area flag:** Besides area numbers, OSPF has different area types. Both routers have to agree on the area type to become neighbors.

    ![OSPF Loopback Interface](https://cdn.networklessons.com/wp-content/uploads/2013/02/ospf-loopback-interface.png)

## Commands

### Basic Setup
```
R1(config)# router ospf 10
R1(config-router)# network 192.168.23.0 0.0.0.255 area 0
q
network 192.168.23.0 0.0.0.255
area 0
router-id 1.1.1.1

# do clear ip ospf process
```
Behind 192.168.23.0 you can see it says 0.0.0.255. This is not a subnet mask but a **wildcard mask**. A wildcard mask is a **reverse subnet mask**.

#### Change default timers
```
R1(config)# interface fastEthernet 1/0
R1(config-if)# ip ospf hello-interval 5
R1(config-if)# ip ospf dead-interval 15
```

#### OSPF Cost
Now what if I wanted to force OSPF to use the slower Ethernet0/0 interface without shutting the FastEthernet interface? It’s possible to manually change the cost, let me show you how:

```
R2(config)#interface fastEthernet 1/0
R2(config-if)#ip ospf cost 50
```

Use the ip ospf cost command to change the cost. When I set it to 50 the FastEthernet interface isn’t attractive anymore.
### Authentication
```
R1(config)# interface fastEthernet 1/0
R1(config-if)# ip ospf authentication message-digest
R1(config-if)# ip ospf message-digest-key 1 md5 mykey

R1(config-if)# router ospf 1
R1(config-router)# area 0 authentication

```
### Show Commands
```
# show ip ospf neighbor
# show ip ospf interface g0/0
# show ip protocols
# show ip route ospf
```