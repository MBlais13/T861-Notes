#cisco #load-balancing

> [!info] Commands
> [[Cisco Commands#OSPF]]

OSPF is a link-state routing protocol.

- OSPF can do MD5 authentication.
- OSPF can do clear text authentication.
- You can enable authentication for the entire area or a single interface.

- IOS(15) supports a maximum of 32 paths for OSPF

---
## Introduction to OSPF
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

## Default Routes
If you use the `**default-information originate**` command, you can advertise a default route in OSPF. OSPF won’t advertise a default route if you don’t already **have it in your routing table**. If you add the `**always**` keyword, it will advertise the default route even if you don’t have it in the routing table.
```
R1(config)#router ospf 1
R1(config-router)#default-information originate ?
  always       Always advertise default route
  metric       OSPF default metric
  metric-type  OSPF metric type for default routes
  route-map    Route-map reference
```
## MD5 Authentication
For MD5 authentication, you need different commands. First, use `**ip ospf message-digest-key X md5**` to specify the key number and password. It doesn’t matter which key number you choose, but it has to be the same on both ends. To enable OSPF authentication, you need to type in **`ip ospf authentication message-digest`.**

```
R1(config)#interface fastEthernet 0/0
R1(config-if)#ip ospf message-digest-key 1 md5 MYPASS
R1(config-if)#ip ospf authentication message-digest
```
^ Do the same for R2

It is also possible to enable authentication for the entire area. This way, you don’t have to use the **`ip ospf authentication message-digest`** command on all of your interfaces to activate it. Here’s the command to enable MD5 authentication for the entire area:

```
R1(config)#router ospf 1
R1(config-router)#area 0 authentication message-digest
```
### MD5 Verification (debug)

```
R1#show ip ospf interface fastEthernet 0/0
FastEthernet0/0 is up, line protocol is up 
  Internet Address 192.168.12.1/24, Area 0 
  Process ID 1, Router ID 192.168.12.1, Network Type BROADCAST, Cost: 1
  Transmit Delay is 1 sec, State BDR, Priority 1 
  Designated Router (ID) 192.168.12.2, Interface address 192.168.12.2
  Backup Designated router (ID) 192.168.12.1, Interface address 192.168.12.1
  Flush timer for old DR LSA due in 00:01:53
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:05
  Supports Link-local Signaling (LLS)
  Index 1/1, flood queue length 0
  Next 0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 1
  Last flood scan time is 0 msec, maximum is 0 msec
  Neighbor Count is 1, Adjacent neighbor count is 1 
    Adjacent with neighbor 192.168.12.2  (Designated Router)
  Suppress hello for 0 neighbor(s)
  Message digest authentication enabled
    Youngest key id is 1
```

Using `**show ip ospf interface**` we see MD5 authentication is enabled, and we are using key ID 1. We have a neighbor, so it seems to be working. Let’s try a debug:

```
R1#debug ip ospf packet 
OSPF packet debugging is on

OSPF: rcv. v:2 t:1 l:48 rid:192.168.12.2
      aid:0.0.0.0 chk:0 aut:2 keyid:1 seq:0x3C7EC653 from FastEthernet0/0
```

Debug shows us that MD5 authentication is enabled (aut:2), and we use key ID 1. Debug is also great for fixing authentication errors. Here’s why:

```
R1(config)#interface fastEthernet 0/0
R1(config-if)#no ip ospf message-digest-key 1 md5 MYPASS  
R1(config-if)#ip ospf message-digest-key 1 md5 MYWRONGPASS
```

First, we’ll enter the wrong password. Now I’ll enable a debug and reset the OSPF process:

```
R1#debug ip ospf adj 
OSPF adjacency events debugging is on
```

```
R1#clear ip ospf process 
Reset ALL OSPF processes? [no]: yes
```

Here’s what you will see:

```
R1#
OSPF: Rcv pkt from 192.168.12.2, FastEthernet0/0 : Mismatch Authentication Key - Message Digest Key 1
```

Somewhere in the debug, you’ll see the message above. This means that we are using MD5 key ID 1 on both sides, but the password is incorrect.  
## Multi-Area Configuration

![ospf two areas multi area](https://cdn.networklessons.com/wp-content/uploads/2017/04/ospf-two-areas-multi-area.png)

Above we have R1 and R2 in area 0, the backbone area. Between R1 and R3, we will use area 1 and between R2/R4 we will use area 2. R3 and R4 have a loopback interface with an IP address that we will advertise in their area.

The network command defines to which area each interface will belong.First, we will configure R1 and R2 for the backbone area:


```
R1(config)#router ospf 1
R1(config-router)#network 192.168.12.0 0.0.0.255 area 0
```

```
R2(config)#router ospf 1
R2(config-router)#network 192.168.12.0 0.0.0.255 area 0
```

Let’s configure R1 and R3 for area 1:

```
R1(config)#router ospf 1
R1(config-router)#network 192.168.13.0 0.0.0.255 area 1
```

```
R3(config)#router ospf 1
R3(config-router)#network 192.168.13.0 0.0.0.255 area 1
R3(config-router)#network 3.3.3.3 0.0.0.0 area 1
```

And last but not least, R2 and R4 for area 2:

```
R2(config)#router ospf 1
R2(config-router)#network 192.168.24.0 0.0.0.255 area 2
```

```
R4(config)#router ospf 1
R4(config-router)#network 192.168.24.0 0.0.0.255 area 2
R4(config-router)#network 4.4.4.4 0.0.0.0 area 2
```

Those are all the network commands we need.
we can verify the configuration with `# show ip ospf neighbor`.
## Reference Bandwidth
OSPF uses a *simple* formula to calculate the OSPF cost for an interface with this formula:
> [!info] Formula
> `cost = reference bandwidth / interface bandwidth`

The reference bandwidth is a value in Mbps that we can set ourselves. By default, this is 100Mbps on Cisco IOS routers. The interface bandwidth is something we can look up.


Use the `**auto-cost reference-bandwidth**` command and specify the value you want in Mbps. Let’s set it to 1000 Mbps:

```
Router(config-router)#auto-cost reference-bandwidth 1000
```
Cisco IOS will warn you that you should do this on all OSPF routers.

Check bandwidth by:
```
Router#show ip ospf | include Reference
	Reference bandwidth unit is 100 mbps
---
R1#show ip ospf interface Serial 0/0 | include Cost
```

##### NOTES
The default reference bandwidth of 100 Mbps can cause issues if you use Gigabit or 10 Gigabit interfaces. The lowest possible cost value is one so with the default reference bandwidth, a FastEthernet, Gigabit, and 10 Gigabit interface would have an OSPF cost of 1.

## Commands

### Basic Setup
```
R1(config)# router ospf 10
R1(config-router)# network 192.168.23.0 0.0.0.255 area 0

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
R2(config)# interface fastEthernet 1/0
R2(config-if)# ip ospf cost 50
```

Use the ip ospf cost command to change the cost. When I set it to 50 the FastEthernet interface isn’t attractive anymore.
#### Authentication
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