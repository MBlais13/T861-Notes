#trunks

> [!info] Commands
> [[Cisco Commands#Trunks]]

Trunks are required to carry VLAN traffic from one switch to another.

---
## Trunking on cisco switch
![[Pasted image 20241011182034.png]]
Trunks let you allow specific vlan traffic on a certain link. Such as having a staff vlan not being able to communicate with students vlan.

## Trunk Encapsulation
Typically dot1q is used.

There are two trunking protocols:

- **802.1Q**: This is the most common trunking protocol. It’s a standard and supported by many vendors.
- **ISL**: This is the Cisco trunking protocol. Not all switches support it.

| type      | description                                                         |
| --------- | ------------------------------------------------------------------- |
| dot1q     | Interface uses only 802.1q trunking encapsulation when trunking     |
| isl       | Interface uses only ISL trunking encapsulation when trunking        |
| negotiate | Device will negotiate trunking encapsulation with peer on interface |
Read more about encapsulation here: [[Encapsulation#Encapsulation Types]]