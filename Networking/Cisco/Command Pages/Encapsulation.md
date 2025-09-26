#tags

> [!info] Commands
> [[Cisco Commands#tag]]

Description

---
## Ethernet Frames
![[Pasted image 20241011194656.png]]
This is a normal ethernet frame. The problem is we don't know what VLAN it belongs to. This means the switch does not know where it belongs.

![[Pasted image 20241011194703.png]]
using `dot1q` allows us to give the frame additional information about where it belongs.

- **VLAN ID:** This is the ID of the vlan the frame belongs to.
- **Priority:** This lets the switch know what priority the frame is, this is useful for voice traffic.
### Encapsulation Types
There are two trunking protocols:

- **802.1Q**: This is the most common trunking protocol. It’s a standard and supported by many vendors.
- **ISL**: This is the Cisco trunking protocol. Not all switches support it.

| type      | description                                                         |
| --------- | ------------------------------------------------------------------- |
| dot1q     | Interface uses only 802.1q trunking encapsulation when trunking     |
| isl       | Interface uses only ISL trunking encapsulation when trunking        |
| negotiate | Device will negotiate trunking encapsulation with peer on interface |


