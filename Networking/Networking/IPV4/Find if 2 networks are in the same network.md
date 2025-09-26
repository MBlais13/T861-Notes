
Question:
```
If the network prefix is /28 are the following 2 IP addresses on the same network: 192.168.67.251 and 192.168.67.56
```
# Step 1
breakdown the question:
prefix: `/28`
network 1: `192.168.67.251`
network 2: `192.168.57.56`

# Step 2
turn everything into binary
prefix: `11111111.11111111.11111111.11110000`
network 1: `11111011`
network 2: `00111000`

# Step 3
compare

take the split octet of your network mask: `11111111.11111111.11111111.(11110000)`

net-mask: `11110000`
network 1: `11111011`
network 2: `00111000`

| net-mask  | **`1`**   | **`1`**   | **`1`**   | **`1`**   | 0   | 0   | 0   | 0   |
| --------- | --- | --- | --- | --- | --- | --- | --- | --- |
| network 1 | **`1`**   | **`1`**   | **`1`**   | **`1`**   | 1   | 0   | 1   | 1   |
| network 2 | **`0`**   | **`0`**   | **`1`**   | **`1`**   | 1   | 0   | 0   | 0   |
This example is `different networks`
* If network bits are the same = `same network`
* If network bits are different = `different networks`