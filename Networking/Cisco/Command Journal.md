>[!info] 28 lines per page


>[!INFO] Syntax
> - Words encased in `__underscores__` are meant to be underlined.
> - Only the first `|` from the left is meant to be the column. Fit the column text at discretion. 
> - 28 writable lines are in the book. some boxes have over 28, they cannot have line breaks with a space above them.
> - when `  └-` is used, it signifies that `R1(whatever)#` will continue to be the same. save the pen ink :) Example Below.
```
Set Defaults | R1(config)# ip dhcp pool MYPOOL
				 | R1(dhcp-config)# default-router 192.168.12.1
				 |				  |-# dns-server 1.1.1.1
				 |				  └-# domain-name example.com
```


---
## Page 1
### Initial Configuration

```txt nums

------------------------------------------------------------------
Hostname		| R1(config)# hostname S1
------------------------------------------------------------------
Banner	#..#	| R1(config)# banner motd #admins only no entry#
------------------------------------------------------------------
Interface Description	| S1(config-if)# Description int desc
------------------------------------------------------------------
logging		| S1(config)# line console 0
synchronous	| S1(config-line)# logging synchronous
------------------------------------------------------------------
set clock		| S1(config)# clock set hh:mm::ss
------------------------------------------------------------------
_save config_  | S1# copy run start
remove config  | S1# erase startup-config
---------------| S1# reload
show config	   | S1# show run
find in config | S1# show run | include default-gateway
------------------------------------------------------------------
disable dns lookup	| S1(config)# no ip domain-lookup
------------------------------------------------------------------







```

---
## Page 2
### Passwords & Security
```txt nums
------------------------------------------------------------------
password secret setup	| S1(config)# enable secret cisco
							 | S1(config)# service password-encryption
secret=enable			| S1(config)# line console 0
password=initial		| S1(config-line)# password 1234
							 | S1(config-line)# login
------------------------------------------------------------------
Set username	| S1(config)# line console 0
& password	| S1(config-line)# login local
				 | S1(config-line)# exit
				 | S1(config)# username admin password cisco
------------------------------------------------------------------
set VTY amount	| S1(config)# line vty 0 4
------------------------------------------------------------------
set VTY password| S1(config)# line vty 0 15
					 | S1(config-line)# password cisco
					 | S1(config-line)# login
------------------------------------------------------------------
Configure SSH	| S1(config)# ip domain-name switch.local
				 | S1(config)# crypto key generate rsa

				 | S1(config)# ip ssh version 2
				 | S1(config)# line vty 0 4
				 | S1(config-line)# transport input ssh
				 | S1(config-line)# login local
				 | S1(config)# username admin secret cisco
------------------------------------------------------------------
Connection	| S1(config)# access-list 1 permit host 192.168.1.2
Access-list	| S1(config)# line vty 0 4
			 	| S1(config-line)# access-class 1 in 
```

---
## Page 3
### DHCP
```txt nums
------------------------------------------------------------------
Prepare		| R1(config)# interface f0/0
interface		| R1(config-if)# no shutdown
				 | R1(config-if)# ip address 192.168.12.1 255.255.255.0
------------------------------------------------------------------
Configure		| R1(config)# ip dhcp pool MYPOOL
DHCP server	| R1(dhcp-config)# network 192.168.12.0 255.255.255.0
------------------------------------------------------------------
Set standard	| R1(dhcp-config)# default-router 192.168.12.1
configuratons| 				  |-# dns-server 1.1.1.1
				 | 				  └-# domain-name example.com
------------------------------------------------------------------
Exclusions	| R1(config)# ip dhcp excluded-address 192.168.12.100
------------------------------------------------------------------
Options		| R1(dhcp-config)# option 150 ip 192.168.12.200
------------------------------------------------------------------
show DHCP		| R1# show ip dhcp binding 
info			| R1# show run | include default-gateway










```

---
## Page 4
### Sub-Interface  &  Routing  &  Next-Hop
```txt nums
Creating a subinterface for `vlan 10` on `g0/0`
------------------------------------------------------------------
Create				| S1(config)# interface g0/0/1.10
Sub Interface	| S1(config-subif)# description default gateway for vlan 10
					 | 					|-# encapsulation dot1q 10
					 | 					└-# ip add 192.168.10.1 255.255.255.0

Show info	 | S1# show ip route
			  | S1# show ip interface br
			  | S1# show interfaces
			  | S1# show interfaces trunk


ROUTING //HEADING
------------------------------------------------------------------
Default Gateway	| S1(config-if)# ip defualt-gateway 192.168.1.1

IP Route	| S1(config)# ip route 10.1.1.0 255.255.255.0 g0/1 
			 | OR S1(config)# ip route 10.1.1.0 255.255.255.0 192.168.1.1


NEXT HOP (static route) //HEADING
------------------------------------------------------------------//UNDERLINE 4 ITEMS BELOW
Interface | ip route, _destinationNetworkIP_, _subnetMaskofDestination_, _nextHopIP_
Next Hop	| S1(config-if)# interface S0/2/0
			 | 				|-# ip route 172.16.20.1 255.255.255.0 209.165.200.226
			 | 				└-# no shut

```

---
## Page 5
### OSPF
```txt nums
a wildcard mask is the inverse of the network mask
------------------------------------------------------------------
Basic	| R1(config)# router ospf 10
Setup	| R1(config-router)# network 192.168.23.0 0.0.0.255 area 0
		 | R1(config-router)# router-id 1.1.1.1
		 
		 | # do clear ip ospf process
------------------------------------------------------------------
Change		| R1(config)# interface fastEthernet 1/0
Default	| R1(config-if)# ip ospf hello-interval 5
Timers		| R1(config-if)# ip ospf dead-interval 15
------------------------------------------------------------------
Reference	| R1(config-router)# auto-cost reference-bandwidth 1000
Bandwidth	| # show ip ospf | include Reference
------------------------------------------------------------------
authentication	| R1(config)# interface fastEthernet 1/0
			| R1(config-if)# ip ospf authentication message-digest
			| R1(config-if)# ip ospf message-digest-key 1 md5 mykey
	
			| R1(config-if)# router ospf 1
			| R1(config-router)# area 0 authentication
------------------------------------------------------------------
Cost	| R1(config)# interface GigabitEthernet0/0
		 | R1(config-if)# ip address 192.168.12.1 255.255.255.0
		 | R1(config-if)# ip ospf cost 10
------------------------------------------------------------------
Passive	| R1(config)# router ospf 10
Interface | R1(config)# passive-interface g0/0
```

---
## Page 6
### Troubleshoot OSPF
```txt nums
a wildcard mask is the inverse of the network mask
------------------------------------------------------------------

show ip ospf neighbor detail
show ip ospf 
























```

---
## Page 7
### Etherchannel  &  Trunks
```txt nums
For LACP use Active / Passive
For PAgP use Auto / Desirable
ON forces etherchannel without LACP or PAgP. only works when two are configured to ON.
------------------------------------------------------------------
Set Interfaces	| S1(config)# int range G0/1 - 2
					 | S1(config-if-range)# channel-group 1 mode active
------------------------------------------------------------------
Create				| S1(config)# interface port-channel 1
Port-channel		| S1(config-if)# switchport mode trunk
					 | S1(config-if)# switchport trunk allowed vlan 1,10,20
------------------------------------------------------------------
load-balancing	| S1(config)#port-channel load-balance ?
TRUNKS //HEADING
------------------------------------------------------------------
Create Trunk		| S1(config) #interface f0/1
					 | S1(config-if)# switchport trunk encapsulation dot1q
					 | S1(config-if)# switchport mode trunk
------------------------------------------------------------------
Assign VLAN	| S1(config-if)# switchport trunk native vlan 10
To Trunk		| OR - S1(config-if)# switchport trunk allowed vlan 10,20,30
				 | 
				 | OR --- enable access with only one vlan
				 | S1(config-if)#switchport mode access
				 | S1(config-if)# switchport access vlan 20
------------------------------------------------------------------
Change			| S1(config)# int f0/1
Encapsulation| S1(config-if)# switchport trunk encapsulation dot1q
______________ //DIVIDE THESE TWO IN THE COLOUMN- NO NEED TO SKIP A LINE
OR FOR			| S1(config)# int f0/1.10
SUBINTERFACE	| S1(config-subif)# encapsulation dot1q 10
```

---
## Page 8
### Port Security  &  CDP
```txt nums

------------------------------------------------------------------
Enable			| S1(config)# interface f0/1
Port-security| S1(config-if)# switchport port-security
				 | 				|-# switchport port-security maximum 1
				 | 				└-# switchport port-security mac-address aaaa.bbbb.cccc

__switchport port-security maximum 1__ makes it so only 1 mac address is allowed.
If returns 'Command rejected: port is dynamic', run __switchport mode access__

------------------------------------------------------------------
Fix disabled	| only doing __no shutdown__ will not work.
interface		| S1(config)# interface f0/1
				 | S1(config-if)# shutdown
				 | S1(config-if)# no shutdown

------------------------------------------------------------------
Show port		| S1# show port-security interface f0/1
Security Info| S1# show port-security addresss

CDP //HEADING
------------------------------------------------------------------
run cdp		| S1(config)# cdp run

show cdp info| S1# show cdp neighbors detail



```

---
## Page 9
### NAT  &  PAT
```txt nums
------------------------------------------------------------------
Static NAT	| R1(config)# interface serial 0/1/0
				 | R1(config-if)# ip address 192.168.1.2 255.255.255.252
				 | R1(config-if)# ip nat inside

				 | R1(config)# interface serial 0/1/1
				 | R1(config-if)# ip address 209.165.200.1 255.255.255.252
				 | R1(config-if)# ip nat outside

				 | R1(config)# ip nat inside source static 192.168.10.254 209.165.201.5
------------------------------------------------------------------
Dynamic NAT | R1(config)# interface serial 0/1/0
			   | R1(config-if)# ip nat inside
			   | 				|-# interface serial 0/1/1
			   | 				└-# ip nat outside
		 	  | 
			   |{R1(config)# ip nat pool NAT-POOL 209.165.200.226 209.165.200.240
			   |{netmask 255.255.255.224
			   | R1(config)# access-list 1 permit 192.168.0.0 0.0.255.255
			   | R1(config)# ip nat inside source list 1 pool NAT-POOL1
------------------------------------------------------------------
PAT		   | __overload__ means include port addresses
			 | R1(config)# ip nat inside source list 1 interface serial 0/1/0 overload
		 	| R1(config)# access-list 1 permit 192.168.0.0 0.0.255.255
		 	| 
			 | R1(config)# interface serial 0/1/1
			 | R1(config-if)# ip nat inside
		 	| 
			 | R1(config)# interface serial 0/1/0
			 | R1(config-if)# ip nat outside
```

---
## Page 10
### SHOW  NAT  &  PAT
```txt nums
------------------------------------------------------------------
Static NAT	| R1(config)# interface serial 0/1/0
				 | R1(config-if)# ip address 192.168.1.2 255.255.255.252
				 | R1(config-if)# ip nat inside

				 | R1(config)# interface serial 0/1/1
				 | R1(config-if)# ip address 209.165.200.1 255.255.255.252
				 | R1(config-if)# ip nat outside

				 | R1(config)# ip nat inside source static 192.168.10.254 209.165.201.5

------------------------------------------------------------------
Show/Verify	| R1# show ip nat translations
Nat InfoR1	| R1# show ip nat translation verbose
				 | R1# show ip nat statistics
				 | R1# show active nat translations
				 | R1# show total nat translations
				 | 
				 | R1# clear ip nat translation *
				 | R1# clear ip nat statistics








```

---
## Page 11
### Standard  ACL
```txt nums
------------------------------------------------------------------
Standard ACL | only permits traffic from network 192.168.12.0 /24
				 | R2(config)#access-list 1 permit 192.168.12.0 0.0.0.255
				 | R2(config)#interface fastEthernet 0/0
				 | R2(config-if)#ip access-group 1 in



------------------------------------------------------------------
Show ACL's	| R2# show access-lists


















```

---







