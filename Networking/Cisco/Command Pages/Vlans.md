#vlans

> [!info] Commands
> [[Cisco Commands#Vlans]]

Description

---
## Vlans Explanation
![[Pasted image 20241011185927.png]]
Vlans (Virtual-LANs) allow you to separate different groups of devices, in most cases isolating say a Finance network from the Sales network

## Vlan Info
By default `VLAN 1` is the native VLAN.
### Vlan location
VLAN information is not saved in the running-config or startup-config but in a separate file called vlan.dat on your flash memory.

If you want to delete the VLAN information, you should delete this file by typing `delete flash:vlan.dat`.
### Configure voice vlan
> [!info] this is beyond the scope of this course

Set ip address of vlan
```
S1(config)# interface f0/1
S1(config-if)# switchport access vlan 30
S1(config-if)# mls qos trust cos
S1(config-if)# switchport voice vlan 150
```

## Inter Vlan issues

| Issue Type                  | How to Fix                                                                                                                                          | How to Verify                                                               |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Missing VLANs               | •Create (or re-create) the VLAN if it does not exist.<br><br>Ensure host port is assigned to the correct VLAN                                       | show vlan [brief]  <br>show interfaces switchport  <br>ping                 |
| Switch Trunk Port Issues    | •Ensure trunks are configured correctly.<br><br>•Ensure port is a trunk port and enabled.                                                           | show interface trunk  <br>show running-config                               |
| Switch Access Port Issues   | •Assign correct VLAN to access port.<br><br>•Ensure port is an access port and enabled.<br><br>•Host is incorrectly configured in the wrong subnet. | show interfaces switchport  <br>show running-config interface  <br>ipconfig |
| Router Configuration Issues | •Router subinterface IPv4 address is incorrectly configured.<br><br>•Router subinterface is assigned to the VLAN ID.                                | show ip interface brief  <br>show interfaces                                |
