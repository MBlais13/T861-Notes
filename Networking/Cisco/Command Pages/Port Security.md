#port-security

> [!info] Commands
> [[Cisco Commands#Port Security]]

We don’t want people to bring their own switches and connect them to our network. Port security will prevent this from happening by locking the interface to only 'talk' to a specified mac address. Anything else will shutdown the interface.

---
## Disabled State
When we send traffic through the secured port on an excluded mac the port goes in `err-disable` state.
```
S1# show port-security interface f0/1
Port Security              : Enabled
Port Status                : Secure-shutdown
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 0
Last Source Address:Vlan   : 0090.cc0e.5023:1
Security Violation Count   : 1
```
```
S1# show interfaces f0/1
FastEthernet0/1 is down, line protocol is down (err-disabled)
```
### Options
```
S1(config-if)# switchport port-security ?
```


### Fix disabled state
To get the interface out of the `err-disabled` state, you need to type `shutdown` followed by `no shutdown`.
- Only typing `no shutdown` is **not enough**!

```
S1(config)# interface f0/1
S1(config-if)# shutdown
S1(config-if)# no shutdown
```