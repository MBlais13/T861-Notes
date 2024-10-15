
# Initial Configuration
## host name
```
Router# conf term
Router(config)# hostname S1
```
## motd / banner
```
S1(config)# banner motd #admins only - no entry#
```
## set VTY
sets amount of sessions 
```
line vty 0 4
```
## Prevent incorrect commands (escape translation)
```
S1(config)# line console 0
S1(config-line)# logging synchronous
```
## set clock time
```
S1(config)# clock set hh:mm::ss
```
---
# Passwords
## enable password
secret = password for 'enable' command
line password = initial connection
```
S1(config)# enable secret cisco
S1(config)# service password-encryption
S1(config)# line console 0
S1(config-line)# password 1234
S1(config-line)# login
S1(config-line)# exit
```
---
# Configure Interface
## add ip route
```
S1(config)# ip route 10.1.1.0 255.255.255.0 g0/1
-- or -- 
S1(config)# ip route 10.1.1.0 255.255.255.0 192.168.1.1
```
## configure interface
```
S1(config)# interface f0/0
S1(config-if)# ip address 172.16.10.1 255.255.255.0
S1(config-if)# no shutdown

S1(config-if)# interface S0/2/0
S1(config-if)# ip address 172.16.20.1 255.255.255.0
S1(config-if)# no shutdown
S1(config-if)# exit
```
## Configure Interface range
Set port settings across multiple ports.
```
S1(config)# interface range f0/1-24
S1(config-if-range)# 
```
## configure interface next hop
`#ip route destinationNetworkIP subnetMaskofDestination nextHopIP`
```
S1(config-if)# interface S0/2/0
S1(config-if)# ip route 172.16.20.1 255.255.255.0 209.165.200.226
S1(config-if)# no shutdown
S1(config-if)# exit

S1# show ip route
```
## default gateway
```
S1(config-if)# ip defualt-gateway 192.168.12.1
```
## remove ip address
```
S1(config-if)# interface S0/2/0
S1(config-if)# no ip address
S1(config-if)# exit
```
---
# Show
## show trunks
```
S1# show int trunk
```
## show vlan
```
S1# show vlan brief
```
## show ip route
```
S1(config-if)# show ip route
```
## show ip addresses
```
S1(config-if)# show ip int br
```
## show interfaces
```
S1# show int br
```
## show running-config
```
S1# show running-config
```
## Show mac address table
```
S1(config)# show mac-address-table
```
---
# Save/Remove Configs
## save config
```
S1# copy running-config startup-config
-- OR --
S1# copy run start
```
## remove config
```
S1# erase startup-config
S1# reload
```
---
# Vlans
## Create vlan
```
S1(config)# vlan 10
S1(config-vlan)# name student
```
## assign vlan to interface
```
S1(config)# int f0/1
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan 10
```
## Show vlan
```
S1# show vlan br
```
## Configure vlan
Change ip address of vlan
```
S1(config)# interface vlan 10
S1(config-if)# ip address 192.168.1.1 255.255.255.0
S1(config-if)# no shut
```
#### Configure native vlan on trunk
```
S1(config)# vlan 10
S1(config-if)# switchport trunk native vlan 10
```
---
# Trunks
## configure vlan trunk
```
S1(config)# int f0/1
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk native vlan 10
S1(config-if)# switchport trunk allowed vlan 10
```
---
# Sub-interface
## sub interface config
```
S1(config)# interface g0/0/1.20
S1(config-subif)# description Default gateway for VLAN 20
S1(config-subif)# encapsulation dot1Q 20
S1(config-subif)# ip add 192.168.20.1 255.255.255.0
S1(config-subif)# exit
```

#### today!!!
```
switchport mode trunk
port-channel 
channel-group 1 mode active
channel-protocol lacp



show int status

show etherchannel summary
```




## Enable SSH
```
S1(config)# 
```


---
# inter-VLAN issues


| Issue Type                  | How to Fix                                                                                                                                          | How to Verify                                                               |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Missing VLANs               | •Create (or re-create) the VLAN if it does not exist.<br><br>Ensure host port is assigned to the correct VLAN                                       | show vlan [brief]  <br>show interfaces switchport  <br>ping                 |
| Switch Trunk Port Issues    | •Ensure trunks are configured correctly.<br><br>•Ensure port is a trunk port and enabled.                                                           | show interface trunk  <br>show running-config                               |
| Switch Access Port Issues   | •Assign correct VLAN to access port.<br><br>•Ensure port is an access port and enabled.<br><br>•Host is incorrectly configured in the wrong subnet. | show interfaces switchport  <br>show running-config interface  <br>ipconfig |
| Router Configuration Issues | •Router subinterface IPv4 address is incorrectly configured.<br><br>•Router subinterface is assigned to the VLAN ID.                                | show ip interface brief  <br>show interfaces                                |
