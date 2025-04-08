#routing #networking 

> [!info] Commands
> [[Cisco Commands#NAT]]

Description

---
## Terminology of NAT:
### Static NAT: 
In Static NAT, IP addresses are statically mapped to each other through manual configuration. Global IP addresses are translated to Local IP addresses based on the statically mapping of these IP addresses.  
There are 2 types of Static NAT: 

1. Inside Static NAT
2. Outside Static NAT
#### Inside Static NAT:
This involves the static mapping of the Inside Local IP address (private address) to the Inside Global address (public address). When Inside Static NAT is used, private IP addresses remain hidden from the outside network.
- **Inside Local:** It is a region inside the Enterprise’s network where the hosts have Private IP addresses.
- **Inside Global:** It is also a region inside the Enterprise network, but Public IP addresses are used in this region (this region is usually connected to the outside network or Internet).
- **Outside Local:** It is a region that is generally part of the Enterprise network but in a public Internet (or outside the Enterprise Network). The hosts of the Outside Local region have private IP addresses.
- **Outside Global**: It is a part of the Enterprise network in a public Internet where Public IP addresses is used.

---
## Configs
### Configuring Static NAT
#### Remove IP Routing
```
Router(config)# no ip routing
```
#### Default Gateway
```
Router(config)# ip default-gateway 192.168.12.2
```
#### Inside and Outside Routing
```
Router(config)# interface fastEthernet 1/0
Router(config-if)# ip nat inside

Router(config)# interface fastEthernet 1/1
Router(config-if)# ip nat outside
```
#### Enable Static NAT
```
Router(config)# ip nat inside source static 192.168.12.1 192.168.23.2
```

### Dynamic NAT
#### Inside and Outside Routing
```
Router(config)# interface fastEthernet 1/0
Router(config-if)# ip nat inside

Router(config)# interface fastEthernet 1/1
Router(config-if)# ip nat outside
```
#### Create pool for global IP addresses
```
Router(config)#ip nat pool <pool-name> 
<starting-IP> <ending-IP> prefix-length <prefix-length>
```
#### Create an ACL
```
Router(config)#access-list <acl-number> 
permit <source-ip-network> <wildcard-mask>
```
#### Enable Dynamic NAT
```
Router(config)#ip nat inside source 
list <acl-number> pool <pool-name>
```
---
### Show Route
```
Router# show ip route
Default gateway is not set

Host               Gateway           Last Use    Total Uses  Interface
ICMP redirect cache is empty
```

```
Router# show ip nat translations 
Pro Inside global      Inside local       Outside local      Outside global
--- 192.168.23.2       192.168.12.1       ---                ---
```