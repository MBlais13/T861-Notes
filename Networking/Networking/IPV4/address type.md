#ipv4

```
broadcast
multicast
unicast
```

| Type | Deffinition |
| ---- | ---- |
| unicast | one-to-one communication |
| multicast | one to many, typically not all |
| broadcast | one to all |
Broadcast is not used in ipv6, see anycast

if network address is all zeros or all ones then it is unicast








**Magic number** 

256 - `X`
Where `X` is the decimal value of the interesting octet. Calculate the subnet id octet as the largest multiple of the magic number that is less than the corresponding ip octet.

### Split octet

Last octet is the last portion 

They flip to become host bits
Flipping 0 > 1

3 remaining in the split octet


**Carryover**
If number is 256, It is too big for the octet and is carried over 256.0 > 0.1

