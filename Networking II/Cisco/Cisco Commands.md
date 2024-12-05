#iOS #cisco 

```sylesheet
S1# 
S1(config)# 
S1(config-line)# 
S1(config-if)# 
```

# Initial Configuration
#### host name
```
R1# conf term
R1(config)# hostname S1
```
#### motd / banner
enclose content in `#...#`
```
S1(config)# banner motd #admins only - no touchi bitch#
```
#### Disable DNS lookup
```
S1(config)# no ip domain-lookup
```
#### set VTY
sets amount of sessions
```
line vty 0 4
```
#### logging synchronous (escape translation)
Prevent incorrect commands, stop cli feed from writing over your input.
```
S1(config)# line console 0
S1(config-line)# logging synchronous
```
#### set clock time
```
S1(config)# clock set hh:mm::ss
```
#### set interface description
```
S1(config-if)# Description this is a description
```
## Save/Remove Configs
#### save config
```
S1# copy running-config startup-config
-- OR --
S1# copy run start
```
#### remove config
```
S1# erase startup-config
S1# reload
```
#### show running-config
```
S1# show running-config
```
### Configure [NTP](NTP.md)
You can also specify a domain.
```
S1(config)# ntp server 192.168.1.1
S1(config)# ntp update-calendar
```
#### Adding NTP redundancy:
```
S2(config)#ntp peer 192.168.1.3
```
#### Check NTP configurations
```
R1# show ntp associations
R1# show ntp status
R1# show clock
R1# show calendar
```


# [[Remote Connection]]
#### Setup SSH
```
S1(config)# ip domain-name switch.local
S1(config)# crypto key generate rsa
The name for the keys will be: S1.switch.local

How many bits in the modulus [512]: 2048
% Generating 2048 bit RSA keys, keys will be non-exportable...
[OK] (elapsed time was 3 seconds)

S1(config)# ip ssh version 2
S1(config)# line vty 0 4
S1(config-line)# transport input ssh
S1(config-line)# login local

S1(config)# username admin secret cisco
```
To skip the interactive `crypto key generate` use
```
S1(config)# crypto key generate rsa general-keys modulus 2048
```
#### Set Access Lists
with an access-list so that you can at least restrict which devices are allowed to connect to your router or switch.
```
S1(config)# access-list 1 permit host 192.168.1.2
R1(config)# line vty 0 4
R1(config-line)# access-class 1 in 
```

# [[Passwords & Security]]
## Setup
#### Initial password secret setup
secret = password for '`Switch> enable`' command
line password = initial connection
```
S1(config)# enable secret cisco
S1(config)# service password-encryption
S1(config)# line console 0
S1(config-line)# password 1234
S1(config-line)# login
S1(config-line)# exit
```
#### Set username & password
Most basic login, asks for username & password on `Switch>` initial connection screen.
 `login local` command tells the switch to refer to a local database of usernames and passwords for authentication.
```
S1(config)#line console 0
S1(config-line)#login local
S1(config-line)#exit
S1(config)#username admin password cisco
```
## Verify info
```
S1# show running-config | include secret
enable secret 5 $1$CANW$U9Y8O6KeFhrFR4l1Qo07h/
---
S1# show running-config | include password
```


# [[Routing]]
#### Default gateway
```
S1(config-if)# ip defualt-gateway 192.168.1.1
```
#### Add ip route
```
S1(config)# ip route 10.1.1.0 255.255.255.0 g0/1
--- 
S1(config)# ip route 10.1.1.0 255.255.255.0 192.168.1.1
```
==are these two ^(above) v(below) the same? why do I have both ip route and next hop?== 
#### Configure interface next hop
`ip route`, `destinationNetworkIP`, `subnetMaskofDestination`, `nextHopIP`
```
S1(config-if)# interface S0/2/0
S1(config-if)# ip route 172.16.20.1 255.255.255.0 209.165.200.226
S1(config-if)# no shutdown
S1(config-if)# exit

S1# show ip route
```
#### Configure interface
```
S1(config)# interface f0/1
S1(config-if)# ip address 172.16.10.1 255.255.255.0
S1(config-if)# no shutdown
```
#### Configure Interface range
Set port settings across multiple ports.
```
S1(config)# interface range f0/1-24
S1(config-if-range)# 
```
#### remove ip address
```
S1(config-if)# interface S0/2/0
S1(config-if)# no ip address
S1(config-if)# exit
```
## Show routing commands
```
S1# show interface brief
S1(config-if)# show ip interface brief
S1(config-if)# show ip route
S1(config)# show mac-address-table

```


# [[DHCP v4]]
## Setup
#### Create a DHCPv4 server
```
--- Prepare interface
R1(config)# interface f0/0
R1(config-if)# no shutdown
R1(config-if)# ip address 192.168.12.1 255.255.255.0
--- Configure DHCP server
R1(config)# ip dhcp pool MYPOOL
R1(dhcp-config)# network 192.168.12.0 255.255.255.0
--- Set standard configuratons
R1(dhcp-config)# default-router 192.168.12.1
R1(dhcp-config)# dns-server 1.1.1.1
R1(dhcp-config)# domain-name example.com
```
#### Set Defaults
```
R1(config)# ip dhcp pool MYPOOL               
R1(dhcp-config)# default-router 192.168.12.1
R1(dhcp-config)# dns-server 1.1.1.1
R1(dhcp-config)# domain-name example.com
```
#### Exclusions
The text only shows this command used **outside** of `dhcp-config`.
```
R1(config)# ip dhcp excluded-address 192.168.12.100
```
#### Options
```
R1(config)# ip dhcp pool MYPOOL
R1(dhcp-config)# option 150 ip 192.168.12.200
```
## Show DHCP info
```
R1# show ip dhcp binding 
Bindings from all pools not associated with VRF:
IP address          Client-ID/	 	    Lease expiration        Type
		    Hardware address/
		    User name
192.168.12.2      0063.6973.636f.2d63.    Sep 13 2024 12:34 PM    Automatic
                    6330.372e.3132.3265.
                    2e30.3030.302d.4661.
                    302f.30
```


# [[SubInterface]]
## Setup
#### Create a subinterface
Creating a subinterface for `vlan 10` on `g0/0`.
Do this for as many vlans you want subinterfaces for.
```
S1(config)# interface g0/0/1.10
S1(config-subif)# description default gateway for vlan 10
S1(config-subif)# encapsulatio dot1q 10
S1(config-subif)# ip add 192.168.10.1 255.255.255.0
```
## Show subinterface info
The following show commands can be used to verify and troubleshoot inter-vlan routing.
```
S1# show ip route
S1# show ip interface br
S1# show interfaces
S1# show interfaces trunk
```

# [[Vlans]]
## Setup
#### Create a Vlan
```
S1(config)# vlan 20
S1(config-vlan)# name students
```
#### Assign a Vlan to interface
```
S1(config)# int f0/1
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 20
```
#### Configure vlan
Set ip address of vlan
```
S1(config)# interface vlan 10
S1(config-if)# ip address 192.168.1.1 255.255.255.0
S1(config-if)# no shut
```
#### Revert vlan port membership
Set ip address of vlan
```
S1(config)# interface f0/1
S1(config-if)# no switchport access vlan
```
#### Disable [[Dynamic Trunking Protocol]]
Enable access mode for inter vlan routing.
```
S1(config-if)# switchport mode access
--- enable access with only one vlan
S1(config-if)# switchport mode access vlan 10
S1(config-if)# no shut
```
## Show vlan info
```
S1# show vlan summary
---
S1# show vlan
VLAN Name                         Status    Ports
---- ---------------------------- -------- ------

1    default                       active    Fa0/3, Fa0/4
		                                      Fa0/5, Fa0/6, Fa0/7

20   Students                      active    Fa0/1, Fa0/2
```

# [[Encapsulation]]
## Setup
This is used in [[Cisco Commands#Trunks]].
#### Change an encapsulation
```
S1(config)# int f0/1
S1(config-if)# encapsulation dot1q 10
---
S1(config-if)# switchport trunk encapsulation dot1q
```
## Show Encapsulation info
#### Show current encapsulation type
```
S1# show interfaces f0/1 switchport
Name: Fa0/14
Switchport: Enabled
Administrative Mode: dynamic auto 
Operational Mode: static access 
Administrative Trunking Encapsulation: dot1q
```
#### Show different encapsulation types
```
S1(config-if)# switchport trunk encapsulation ?
```


# [[Etherchannel]]
## Setup
Commands relating to setup of Etherchannel
- For AutoNegotiation refer to [this page](Etherchannel.md#AutoNegotiation)

==The layout for basic setup seems weird, commands are correct though==
#### Basic Setup
> **Step One:** Specify the interfaces that compose the etherchannel group.

For [LACP](Etherchannel.md#LACP) use `Active` instead of `desirable`
```
S1(config)# int range G0/1 - 2
S1(config-if-range)# channel-group 1 mode active
```
The switch then automatically creates a new port-channel interface.
Do the same on switch S2
> **Step Two:** Create the port channel interface.
> **Optional:** Then specify vlans and other layer 2 data.

```
S1(config)# interface port-channel 1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk allowed vlan 1,10,20
```
#### configure load-balancing
Change the default behavior of the etherchannel load-balancing.
```
S1(config)#port-channel load-balance ?
  dst-ip       Dst IP Addr
  dst-mac      Dst Mac Addr
  src-dst-ip   Src XOR Dst IP Addr
  src-dst-mac  Src XOR Dst Mac Addr
  src-ip       Src IP Addr
  src-mac      Src Mac Addr
```
## Show etherchannel info
```
S1# show run interface G0/1

interface GigabitEthernet0/1
   channel-group 1 mode desirable
end
```

```
S1#show etherchannel summary 
-----------------------------------------------------
1      Po1(SU)         LACP      Gi0/1(P)    Gi0/2(P)
```

```
SW1#show etherchannel 1 port-channel
         Port-channels in the group: 
         ---------------------------

Port-channel: Po1    (Primary Aggregator)

------------

Age of the Port-channel   = 0d:00h:01m:43s
Logical slot/port   = 16/0          Number of ports = 2
HotStandBy port = null 
Port state          = Port-channel Ag-Inuse 
Protocol            =   LACP
Port security       = Disabled
Load share deferral = Disabled   

Ports in the Port-channel: 

Index   Load   Port     EC state        No of bits
------+------+------+------------------+-----------
  0     00     Gi0/1    Active             0
  0     00     Gi0/2    Active             0

Time since last port bundled:    0d:00h:01m:04s    Gi0/2
```

#### Show load-balancing
This shows us that Etherchannel is load-balancing based on the source MAC address.
```
SW1#show EtherChannel load-balance 
EtherChannel Load-Balancing Configuration:
      src-mac

EtherChannel Load-Balancing Addresses Used Per-Protocol:
Non-IP: Source MAC address
  IPv4: Source MAC address
  IPv6: Source MAC address
```
# [[Trunks]]
## Setup
#### Create Trunk
Before setting mode to trunk, you need to set trunk encapsulation.
different encapsulation types: [[Trunks#Trunk Encapsulation]]

```
S1(config) #interface f0/1
S1(config-if)# switchport trunk encapsulation dot1q
S1(config-if)# switchport mode trunk
```
#### Assign vlan for trunk
```
S1(config-if)# switchport trunk native vlan 10
--
S1(config-if)# switchport trunk allowed vlan 10,20,30
--
possibly wrong (review #DTP)???? S1(config-if)# switchport access vlan 20
```
#### Disable [[Dynamic Trunking Protocol]]
```
S1(config-if)#switchport mode access
--- enable access with only one vlan
S1(config-if)#switchport mode access vlan 10
```
## Show trunk info
Show trunk status along with vlans and encapsulation type
```
S1# show interface trunk
--- 
S1# show interface fa0/14 trunk
Port        Mode             Encapsulation  Status        Native vlan
Fa0/14      on               802.1q         trunking      1
Port        Vlans allowed on trunk
Fa0/14      1-4094
Port        Vlans allowed and active in management domain
Fa0/14      1,50
Port        Vlans in spanning tree forwarding state and not pruned
Fa0/14      50
```



# [[Port Security]]
## Setup
#### Enable port security
```
S1(config)# interface f0/1
S1(config-if)# switchport port-security
S1(config-if)# switchport port-security maximum 1

S1(config-if)# switchport port-security mac-address aaaa.bbbb.cccc
```
`switchport port-security maximum 1` makes it so only 1 mac address is allowed.
If returns `Command rejected: port is dynamic`, run `switchport mode access`
#### Fix disabled interface
- only doing `no shutdown` **will not work**
```
S1(config)# interface f0/1
S1(config-if)# shutdown
S1(config-if)# no shutdown
```
## Show command info
```
S1# show port-security interface f0/1
---
S1# show port-security addresss
```


# Logs and Monitoring

## [[RMON]]
### Start RMON
Cannot enable it on SVI (switch virtual interface) interfaces.
```
S1(config-if)# rmon collection history 1 interval 5
```
### Show RMON stats & history
```
S1# show rmon statistics 
S1# show rmon history
```

## [[Syslog]]
### Syslog Server
```
S1(config)# logging 192.168.1.8
```
### Syslog Options
```
S1(config)# service sequence-numbers 
S1(config)# no service timestamps
S1(config)# logging buffered warnings 
S1(config)# logging buffered 16384
```
### View Syslog
```
S1(config)# logging console debugging 
S1(config)# logging monitor debugging 
S1# show logging
S1(config)#logging trap informational
R1#show logging | include Log Buffer
```




# make notes - temp
```
show mac address-table dynamic
--
HSRP / FHRP
--
dhcp snooping
Note: DHCP snooping is required by Dynamic ARP Inspection (DAI)
--
arp inspection
--
configure PortFast
--
Spanning-Tree + summary
--
Portfast & BPDU Guard notes
```

# skills test 1
```
trunking
etherchannel lacp OR pagp
encapsulation
setting ip address
set native vlan
switchport mode trunk native vlan 10,20,30
create sub interfaces
create & set vlans
```

# skills test 2
```
Create DHCP pools and configure them
Set excluded DHCP addresses
Set default and static routes
Enable port security and configure some settings
Remote into a WLC, and create a WLAN, DHCP, and Interface
Connect a host to a wireless network
```
[[#DHCP v4]]
[[#Routing]]
[[#Port Security]]

