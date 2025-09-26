#NTP #networking

> [!info] Commands
> [[Cisco Commands#Configure [NTP](NTP.md)]]

NTP (Network Time Protocol) is used to allow network devices to synchronize their clocks with a central source clock.

---
## About NTP
NTP uses a concept called “stratum” that defines how many NTP hops away a device is from an authoritative time source.

For example, a device with stratum 1 is a very accurate device and might have an atomic clock attached to it. Another NTP server using this stratum 1 server to sync its own time would be a stratum two device because it’s one NTP hop further away from the source.

Cisco routers and switches can use three different NTP modes:
- NTP client mode.
- NTP server mode.
- NTP symmetric active mode.

The symmetric active mode is used between NTP devices to synchronize with each other, it’s used as a backup mechanism when they are unable to reach the (external) NTP server. [[#NTP redundancy]]
### NTP server configuration
Verify your sw/router can resolve hostnames before configuring.
```
R1(config)# ip name-server 8.8.8.8
R1(config)# ntp server pool.ntp.org
R1(config)# ntp update-calendar
```
update-calendar updates the hardware clock with the software clock.

### NTP redundancy
`ntp peer` will allow them to use each other for synchronization. This is the symmetric active mode, basically the two switches will “help” each other to synchronize…this might be useful in case the NTP server fails someday.
```
SW1(config)#ntp peer 192.168.1.2
```

```
SW2(config)#ntp peer 192.168.1.3
```

### Other NTP features
Other things I might add in the future.
- Multicast and Broadcast with NTP
- NTP Authentication
- NTP Access-Control
Bet you didn't know there could be so much stuff involved with a time protocol.