#DTP

> [!info] Commands
> [[Cisco Commands#Disable Dynamic Trunking Protocol]]

DTP is enabled by default, this means when your switchport receives a DTP packet, your interface will enable trunk mode.

---
## DTP defaults
* Depending on the switch model and IOS version, the default might be “dynamic auto” or “dynamic desirable”.

By default, DTP is enabled, and the interfaces of your switches will be in “dynamic auto” or “dynamic desirable” mode. This means that your interface will be in trunk mode whenever you receive a DTP packet that requests to form a trunk.


There are two ways to disable DTP negotiation:

- Configure the interface for access mode.
- Use the `switchport nonegotiate` command on the interface.
### Commands for DTP
#### Show DTP status
```
S1# show interfaces f0/1 switchport
Name: F0/1
Switchport: Enabled
Administrative Mode: dynamic auto
Operational Mode: static access
Administrative Trunking Encapsulation: negotiate
Operational Trunking Encapsulation: native
Negotiation of Trunking: On
```
#### Turn off DTP
```
S1(config)# interface f0/1
S1(config-if)# switchport mode access 
```
Turning off DTP will display
```
S1# show interfaces fastEthernet 0/1 switchport 
Name: Fa0/1
Switchport: Enabled
Administrative Mode: static access
Operational Mode: static access
Administrative Trunking Encapsulation: negotiate
Operational Trunking Encapsulation: native
Negotiation of Trunking: Off
```

