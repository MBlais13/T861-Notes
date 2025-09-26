

address blocks

| class | type                          | name           |
| ----- | ----------------------------- | -------------- |
| A     | 10.0.0.0 - 10.255.255.255     | 10.0.0.0/8     |
| B     | 172.16.0.0 - 172.31.255.255   | 172.16.0.0/12  |
| C     | 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 |
## NAT

The primary use of NAT is to conserve public IPv4 addresses.

NAT allows networks to use private IPv4 addresses internally and translates them to a public address when needed.

A NAT router typically operates at the border of a stub network.

When a device inside the stub network wants to communicate with a device outside of its network, the packet is forwarded to the border router which performs the NAT process, translating the internal private address of the device to a public, outside, routable address.

## Types of NAT
- Static NAT
	One to one mapping that remain constant
	
- Dynamic NAT
	Uses a pool of public addresses and assigns them on a first-come, first served basis
	
- PAT (Port Address Translation)
	Also known as NAT-Overload, maps to multiple private IPV4 addresses to a single or a few public IPV4 addresses.
	
- Next Available Port
	Attempts to reserve the original source port, if already used, PAT assigns the first available port number starting from the beginning of the appropriate port group.
	
	When no more ports are available, PAT moves to the next address to try to allocate the original source port.

| Inside Global IP Address | Inside Local IP Address |
| ------------------------ | ----------------------- |
| 209.165.200.226:1444     | 192.168.10.11:1444      |
| 209.165.200.226:1445     | 192.168.10.12:1444      |

