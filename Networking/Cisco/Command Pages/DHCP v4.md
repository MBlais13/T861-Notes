#DHCP

> [!info] Commands
> [[Cisco Commands#DHCP v4]]

Dynamically set IPv4 addresses for devices on your network without going into the nitty gritty details. 

---
## DHCP server
![[Pasted image 20241013235007.png]]

### Options (VoIP/WAP)
If you have VoIP phones or wireless access points, you probably have to use the “option” fields when giving IP addresses to devices.
```
R1(config)# ip dhcp pool MYPOOL
R1(dhcp-config)# option 150 ip 192.168.12.200
```
Option 150 is used by Cisco IP phones to locate the TFTP server so that they can get their configuration files. The `option` command tells the IP phones to go to the TFTP server with IP address 192.168.12.200.