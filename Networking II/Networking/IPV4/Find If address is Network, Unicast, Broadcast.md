



Find if network address is `network`,`unicast`, or `broadcast`.

* convert up & subnet to binary
* look exactly above 0s in host position


`11000000.10101000.10010000.11100111`
This example is `unicast`
* If all bits in ip are 0 = `network`
* If all bits in ip are 1 = `broadcast`
* If anything else = `unicast`


subnet mask = `11111111.11111111.11111111.(11100000)`
ipv4 binary = `11000000.10101000.10010000.11100111`

192.168.144.231


---
# Step 1
Convert IP address to binary

192.168.144.231

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   | 1   | 0   | 0   | 1   | 1   | 1   |
$$
128+64+32+16+4+2+1 = 231
$$
`11000000.10101000.10010000.11100111`


# Step 2

Find the split octet In your subnet mask
`11111111.11111111.11111111.(11100000)`

take you ipv4 binary and look at your split octet
`11000000.10101000.10010000.(11100111)`

This example is `unicast`
* If all bits in ip are 0 = `network`
* If all bits in ip are 1 = `broadcast`
* If anything else = `unicast`