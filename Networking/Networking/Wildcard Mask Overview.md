#networking #acl

- wildcard mask bit 0 - Must match the bit value in address
- wildcard mask bit 1 - Ignore the bit value in address

`HOST` keyword represents `0.0.0.0` States that all IPV4 addresses must match the bits. 
`ANY` keyword represents `255.255.255.255` 

command usage:
```
Router(config)# access-list {access-list-number} {deny | permit | remark} source [source-wildcard] [log]
```

```
Router(config-if)# ip access-group {access-list-number | access-list-name} {in | out}
```

```
access-list 10 permit 192.168.16.0 0.0.15.255
```


|                    |                                                  |
| ------------------ | ------------------------------------------------ |
| access-list-number | Number range 1-99 or 1300-1999                   |
| remark             | (optional) description                           |
| source-wildcard    | (optional) 32bit wildcard mask applied to source |

```
Router(config)# do show access-lists
--
Router# show run | section access-list
--
Router# show ip S0/1/0 | include access list
```