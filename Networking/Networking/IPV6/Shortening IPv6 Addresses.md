#ipv6 

IPv6 addresses are hexadecimal and since they are 128-bit, they are very long. To fix this IPv6 addresses can be shortened.

>[!info] Naming Scheme
>When we talk about IPv4 addresses, we use the term 'octet' of 8 bits. In IPv6 the official term for 4 hexadecimal values is 'hexadectet', this is hard to remember/pronounce so the short form 'hextet' will be used.


- **Original**: 2041:0000:140F:0000:0000:0000:875B:131B
- **Short**: 2041:0000:140F::875B:131B

If there is a **string of zeros then you can remove them once**. Above I removed the entire 0000:0000:0000 part. You can only do this **once**, your IPv6 device will fill up the remaining space with zeros until it has a 128 bit address.

There is more however, the address can be shortened even more:

- Short: 2041:0000:140F::875B:131B
- Shorter: 2041:0:140F::875B:131B

If you have a “hextet” with 4 zeros then you can remove those and leave a single zero.





Leading zeros can also be removed:

- Original: 2001:0001:0002:0003:0004:0005:0006:0007
- Short: 2001:1:2:3:4:5:6:7

By removing these zeros we get a nice short IPv6 address.


### Summary
- An entire string of zeros can be removed, you can only do this once.
- 4 zeros can be removed, leaving only a single zero.
- Leading zeros can be removed.
- A string of at least two sets of zeros such as `:0000:0000:` can be replaced with `::` but a single string of zeros such as `:0000:` can only be replaced with `:0:`

