#CDP

> [!info] Commands
> [[Cisco Commands#CDP]]

Most networks have multiple switches and/or routers and to make our life easier it’s good to have a network map that shows us how everything is connected to each other, what kind of devices we have, to what VLAN they belong, and the IP addresses that we are using. CDP is a Cisco protocol that runs on all Cisco devices that helps us discover Cisco devices on the network. CDP is Cisco proprietary, runs on the data-link layer, and is enabled by default.

---
## Heading

![cdp demo topology](https://cdn.networklessons.com/wp-content/uploads/2013/02/cdp-demo-topology.png)

Above we have 3 routers. Now if I had no idea what the network looked like we could use CDP to build the network map that you see above. Let me show you how:

```
R1# show cdp neighbors 
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater

Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
R2               Ser 0/0            167        R S I      3640      Ser 0/0
```

Use the `**show cdp neighbors**` command to see all **directly connected** neighbors. Above you see that R1 is connected to R2 and you can also see the platform (3640 router) and the interfaces on both sides. Let me show you the other routers as well:

```
R2# show cdp neighbors 
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater

Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
R1               Ser 0/0            144        R S I      3640      Ser 0/0
R3               Fas 1/0            164        R S I      3640      Fas 1/0
```

```
R3# show cdp neighbors 
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater

Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
R2               Fas 1/0            135        R S I      3640      Fas 1/0
```

Now we have all the information we need to build a network map with the router names and interfaces. CDP can tell us even more, however…

```
R1# show cdp neighbors detail 
-------------------------
Device ID: R2
Entry address(es): 
  IP address: 192.168.12.2
Platform: Cisco 3640,  Capabilities: Router Switch IGMP 
Interface: Serial0/0,  Port ID (outgoing port): Serial0/0
Holdtime : 136 sec

Version :
Cisco IOS Software, 3600 Software (C3640-JK9O3S-M), Version 12.4(16), RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2007 by Cisco Systems, Inc.
Compiled Wed 20-Jun-07 11:43 by prod_rel_team

advertisement version: 2
VTP Management Domain: ''
```

Use `**show cdp neighbors detail**` to reveal even more information. For example, you can see the IP address and the IOS version. This can be very useful to us, but it’s also a security risk. By default, CDP is enabled and runs on all interfaces, so it might be a good idea to disable it on certain interfaces:

```
R1(config)# interface serial 0/0
R1(config-if)# no cdp enable
```

This is how you can disable it for a single interface, just type `no cdp enable`. This is how you can do it globally for all interfaces:

```
R1(config)# no cdp run
```

That’s all there is to CDP. Besides revealing networking information, CDP is also used for Cisco IP phones. Keep in mind that CDP only runs on Cisco hardware, there’s also a “standards” based version called [LLDP](https://networklessons.com/cisco/ccna-200-301/link-layer-discovery-protocol-lldp) that runs on Cisco hardware and some other networking vendor equipment.  

-   Configurations
-   R3
-   R1
-   R2
