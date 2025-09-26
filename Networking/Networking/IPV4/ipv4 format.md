#ipv4 


>[!adress bits]
>IPV4 addresses have `4 octets` with `8 bits` in each octet
>Totalling `32 bits` for the entire address
>```
>8bits . 8bits . 8bits . 8bits
>```
>The first 24 bits are the Network Address while the last 8 bits are the Host Address

| Network Bits/Address | Host Bits/Address |
| ---- | ---- |
| 192.168.1 | .1 |
## Subnetting Breakdown
| # of hosts | # of host bits | network address | prefix | subnet mask | broadcast address | first host | last host | magic number | split octet |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1417 | 11 |  |  |  |  |  |  |  |  |
#### Number of Hosts
The number of hosts is the amount of clients you will base your network to support.
It is necessary to know the number of hosts when building a network.

#### Number of Host Bits
The number of host bits is determined by the [[#Number of Hosts]].
To find the Number of host bits: $2^y - 2=x$ where $x$ is the number of hosts without going under after subtracting. 

#### Network Address
The network address is the address of your network such as `192.168.1.0`

#### Prefix
The prefix is: `Number of Host Bits - 32` . This is because the max number of bits is 32 in ipv4.

#### Subnet Mask


#### Broadcast Address
The absolute last ip address in a network range is reserved for the broadcast address.

#### First Host
The first available address able to be given out to a client.

#### Last Host
The last available address able to be given out to a client.

#### Magic Number


#### Split Octet



## Example Network
Here is a basic home network.

| Example Network | Values |
| ---- | ---- |
| Netmask | 192.168.1.0/24 |
| Network address | 192.168.1.0 |
| Network mask | 255.255.255.0 |
| Network mask in binary | 11111111.11111111.11111111.00000000 |
| CIDR notation | /24 |
| Wildcard mask | 0.0.0.255 |
| Network size | 256 |
| First address | 192.168.1.1 |
| Last address | 192.168.1.254 |
| Broadcast address | 192.168.1.255 |
| IP class | C |
