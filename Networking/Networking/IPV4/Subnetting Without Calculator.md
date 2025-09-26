#ipv4 #subnetting 

## Network Classes
| Class | Format                       | Default Net Mask |
| ----- | ---------------------------- | ---------------- |
| A     | network.node.node.node       | 255.0.0.0        |
| B     | network.network.node.node    | 255.255.0.0      |
| C     | network.network.network.node | 255.255.255.0    |

# Subnetting Breakdown

### Starting Values
The [[#Number of hosts]] and the starting network address are given.
Starting Address: `172.16.0.0/16`

| number of hosts | number of host bits | network address | prefix | subnet mask   | broadcast address | first host  | last host     | magic number | split octet |
| --------------- | ------------------- | --------------- | ------ | ------------- | ----------------- | ----------- | ------------- | ------------ | ----------- |
| 2594            | 12                  | 172.16.0.0      | 20     | 255.255.240.0 | 172.16.15.255     | 172.16.0.1  | 172.16.15.254 |              |             |
| 973             | 10                  | 172.16.16.0     | 22     | 255.255.252.0 | 172.16.19.255     | 172.16.16.1 | 172.16.19.254 |              |             |
| 101             | 7                   |                 | 25     |               |                   |             |               |              |             |
| 93              | 7                   |                 | 25     |               |                   |             |               |              |             |
| 2               | 2                   |                 | 30     |               |                   |             |               |              |             | ^BcouY3zq

### Number of hosts
These are the number of clients per network. These will be given.

### Number of Host Bits
The number of host bits is determined by the [[#Number of Hosts]].
To find the Number of host bits: $2^y - 2=x$ where $x$ is the number of hosts without going under after subtracting. 

For example the first line with `2594` hosts would be: `2^12 - 2 = 4094`. since `4094` is the closest we can get to `2594` without going over, `12` is the [[#Number of Host Bits]] we use.
Continue this method down the rows

| **Number of host bits** | 14    | 13   | 12   | 11   | 10   | 9   | 8   | 7   | 6   | 5   | 4   | 3   | 2   |
| ----------------------- | ----- | ---- | ---- | ---- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
| **$2^n$**               | 16384 | 8192 | 4096 | 2048 | 1024 | 512 | 256 | 128 | 64  | 32  | 16  | 8   | 4   |
| **number of hosts**     | 16382 | 8190 | 4094 | 2046 | 1022 | 510 | 254 | 126 | 62  | 30  | 14  | 6   | 2   |
| Prefix ($32-$host bits) | 18    | 19   | 20   | 21   | 22   | 23  | 24  | 25  | 26  | 27  | 28  | 29  | 30  |

### Prefix (CIDR)
The Prefix can also sometimes be referred to as a CIDR (Classless Inter-Domain Routing)

To get the prefix take the [[#Number of Host Bits]] and subtract it by `32`.

---
### Converting Ip Address To Binary
Table for converting `Decimal` to `Binary`.

```
172.16.0.0
```

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 0   | 1   | 0   | 1   | 1   | 0   | 0   |
$$
128+32+8+4 = 172
$$

| IP                 | 172**.** | 16**.**  | 0**.**   | 0        |
| ------------------ | -------- | -------- | -------- | -------- |
| Binary IP          | 10101100 | 00010000 | 00000000 | 00000000 |
| Binary Subnet Mask | 11111111 | 11111111 | 00000000 | 00000000 |
| Subnet Mask        | 255**.** | 255**.** | 0**.**   | 0        |


### Subnet Mask
when a net mask value is `255` that means that octet is not changeable(fixed).
For example: `172.16.0.0`, if the subnet mask was `255.255.0.0` that would mean that network portion is unchangeable (`172.16`) whereas the host portion is able to take any value such. It would be given a range of `172.16.0.0 - 172.16.255.255`

To find the subnet mask take the [[#Prefix]] number example `20` and mark the first 20 bits as `1`.
Then convert binary to human readable: `11111111.11111111.11110000.00000000` would be = `255.255.240.0`.

```
20 bits = 11111111.11111111.11110000.00000000 = 255.255.240.0
```
### Magic Number
| Octet              | 1        | 2        | 3        | 4        | split octet |
| ------------------ | -------- | -------- | -------- | -------- | ----------- |
| Binary Subnet Mask | 11111111 | 11111111 | 11111100 | 00000000 |             |
| split octet        |          |          | 2^2=2    |          | 3           |
| Binary Subnet Mask | 11111111 | 11111111 | 11111111 | 00000000 |             |
| split octet        |          |          | 2^0=1    |          | 3           |


```
2^ the amount of zeros in the split octet
```

## Notable References
* https://community.spiceworks.com/topic/1838568-the-easy-way-to-calculate-ipv4-subnets-in-your-head
* https://www.techtarget.com/searchnetworking/tip/IP-addressing-and-subnetting-Calculate-a-subnet-mask-using-the-hosts-formula





