#cisco #switching #load-balancing

> [!info] Commands
> [[Cisco Commands#Etherchannel]]

Etherchannel is also known as **link aggregation**. EtherChannel lets you bundle multiple physical links into a single link.

- Etherchannel is cisco proprietary for link aggregation

---
## Problem and solution
### Problem
Original network diagram with network congestion. This is a problem because the link between SW1 and SW2 will become saturated quickly.
![[Pasted image 20241011155025.png]]

---
### Solutions
There are two solutions to this problem:
- Replace the link between the switches with a higher bandwidth, perhaps a 10G link.
- Add multiple links and bundle them into an EtherChannel(aggregate them together).
---

![[Pasted image 20241011154901.png]]
The problem with the image above is even though there are multiple links, we have now created a loop. The spanning-tree protocol would block one of the links.

---
### end result
Etherchannel bundles the two links together using load balancing. Now we have redundancy in case one of the links fails, **it will keep working and use the links that we have left.

> [!info] Keep in mind
> A single traffic flow wont be able to exceed the speed of one link. Etherchannel is the equivalent of adding more lanes to a highway, increasing bandwidth but the speed limit does not change.

![[Pasted image 20241011154908.png]]

---
### Technology

If you want to configure an EtherChannel then we have three options:

- **PAgP (Cisco proprietary)**
- **LACP (IEEE standard)**
- **Manual**
It’s also possible to configure a static EtherChannel without these protocols doing the negotiation of the link for you.


If you are going to create an EtherChannel you need to make sure that all interfaces have the same configuration:

- Duplex.
- Speed.
- Native and allowed VLANs.
- Switchport mode (access or trunk).

Interface types cannot be mixed. Fast Ethernet and Gigabit Ethernet cannot be mixed within a single EtherChannel.


PAgP and LACP will check if the configuration of the interfaces that you use is the same.

---
## AutoNegotiation
**TLDR**; Basically desirable ONLY wants to have sex, auto can have sex if you ask it to, and the other one doesn't want sex.

It is also possible to configure a static or unconditional EtherChannel without PAgP or LACP.
### PAgP
PAgP is cisco proprietary for LACP

| S1        | S2             | Channel Establishment |
| --------- | -------------- | --------------------- |
| On        | On             | Yes                   |
| On        | Desirable/Auto | No                    |
| Desirable | Desirable      | Yes                   |
| Desirable | Auto           | Yes                   |
| Auto      | Desirable      | Yes                   |
| Auto      | Auto           | No                    |

### LACP

| S1      | S2             | Channel Establishment |
| ------- | -------------- | --------------------- |
| On      | On             | Yes                   |
| On      | Active/Passive | No                    |
| Active  | Active         | Yes                   |
| Active  | Passive        | Yes                   |
| Passive | Active         | Yes                   |
| Passive | Passive        | No                    |

---
## load-balancing
#load-balancing 
![[Pasted image 20241011175550.png]]
By default Etherchannel will load-balance based on mac address.

We can change this behavior to one of the following options with this command: [[Cisco Commands#change load-balancing]].

|             |                      |
| ----------- | -------------------- |
| dst-ip      | Dst IP Addr          |
| dst-mac     | Dst Mac Addr         |
| src-dst-ip  | Src XOR Dst IP Addr  |
| src-dst-mac | Src XOR Dst Mac Addr |
| src-ip      | Src IP Addr          |
| src-mac     | Src Mac Addr         |

