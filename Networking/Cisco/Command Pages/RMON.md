#Monitoring #Logs 

> [!info] Commands
> [[Cisco Commands#RMON]]

RMON allows you to monitor things like the CPU or looking for the number of incoming packets on an interface.
Cisco Catalyst switches support some RMON features that allow you to collect more information about packets that arrive on your interfaces.

---
## About RMON
If you want to enable RMON you have two options:

- **Native Mode** (Analyze packets that are destined for your interface).
- **Promiscuous Mode** (Analyze all packets that you encounter on the segment).

You can enable this for switch ports (layer 2) or routed ports (layer 3), but it’s impossible to enable it on SVI (switch virtual interface) interfaces.

- Enabling RMON does use additional system and CPU resources.
## Exploring RMON
See RMON modes
```
S1(config)# interface f0/1
S1(config-if)# rmon ?
  collection      Configure Remote Monitoring Collection on an interface
  native          Monitor the interface in native mode
  promiscuous     Monitor the interface in promiscuous mode
```

This is to configure how often and how much statistics we want to collect:
```
S1(config-if)# rmon collection history 1 ?
  buckets   Requested buckets of intervals. Default is 50 buckets
  interval  Interval to sample data for each bucket. Default is 1800 seconds
  owner     Set the owner of this RMON collection
  <cr>
```

The '`1`' is the RMON collection control index. You can pick any value you like. By default RMON will sample data every 1800 seconds..this is a little too long for my example, so I’ll reduce it to 5 seconds:
```
Switch(config-if)# rmon collection history 1 interval 5
```

## RMON statistics & history
#### Statistics
```
S1# show rmon statistics 
Collection 10006 on FastEthernet0/1 is active, and owned by config,
 Monitors ifIndex.10006 which has
 Received 34577 octets, 441 packets,
 39 broadcast and 395 multicast packets,
 0 undersized and 0 oversized packets,
 0 fragments and 0 jabbers,
 0 CRC alignment errors and 0 collisions.
 # of dropped packet events (due to lack of resources): 0
 # of packets received of length (in octets):
  64: 65, 65-127: 368, 128-255: 5,
  256-511: 1, 512-1023: 2, 1024-1518:0
```
#### History
```
S1# show rmon history 
Entry 1 is active, and owned by 
 Monitors ifIndex.10001 every 5 second(s)
 Requested # of time intervals, ie buckets, is 50,
  Sample # 1 began measuring at 04:03:20
   Received 5002 octets, 58 packets,
   4 broadcast and 54 multicast packets,
   0 undersized and 0 oversized packets,
   0 fragments and 0 jabbers,
   0 CRC alignment errors and 0 collisions.
   # of dropped packet events is 0
   Network utilization is estimated at 0
  Sample # 2 began measuring at 04:03:25
   Received 4732 octets, 64 packets,
   3 broadcast and 59 multicast packets,
   0 undersized and 0 oversized packets,
   0 fragments and 0 jabbers,
   0 CRC alignment errors and 0 collisions.
   # of dropped packet events is 0
   Network utilization is estimated at 0
```