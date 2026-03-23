
His email states:
The test will cover all material covered thus far including:
- Intro to Wireshark / HTTP(S)
- Packet Analysis and Network Basics
- Tapping the wire
- Working with capture packets (including both display and capture filters)
- Advanced Wireshark features
- Packet Analysis from command line
- Subnetting
- Route Summary




Display filters
Source
Dest
Capture filters
TCP and dst tcp port
Test questions on command line arguments
Describe encapsulation process OSI/TCP
OSI model
Know wireshark options
Know what graph to use and when
How to sniff a network and when to sniff
Subnetting & route summary
VLSM

22 questions all short answer


https://www.ibm.com/docs/en/qsip/7.4.0?topic=queries-berkeley-packet-filters


### Capture Filters
```
src host $ip_val
dst host $ip_val
ether [src|dst] host $etherhost
src port $port_val 
dst port $port_val
tcp [src|dst] port $port_val
udp [src|dst] port $port_val
host $ip_val and port $port_val
```

### Display Filters
```
ip.src 
ip.dst 
ip.addr

eth.src
eth.dst 
eth.addr

tcp.srcport 
tcp.dstport 
tcp.port

udp.srcport 
udp.dstport 
udp.port
```

---

## Packet Analysis
protocols
ARP, DNS, TCP, UDP, HTTP, TLS

simple ports
- http/s = 80,443
- ssh = 22
- dns = 53
- rdp = 3389

performance
latency, loss, throughput

## OSI model
application data
L4 - adds TCP/UDP ports headers = **Segment(TCP) / Datagram(UDP)**
L3 - adds ip header = **Packet**
L2 - adds ethernet header/trail MAC + FCS = **Frame**
L1 - bits through the cable = **Bits**

## Tapping the wire & how to sniff
Span / Port mirror
- the switch will copy traffic from one or more ports/vlans to your capture port

network tapp
- physically duplicates traffic via hardware

host-based capture
- capture on the endpoint device
- can only view devices that it can see

when to sniff
- slow, latency, loss, DNS issues
- intermittent disconnects
- investigate security
- verify network changes

## working with capture packets
display filter = wireshark language
capture filter = BPF (during capture)

Example **show packets from**
show packets to/from 192.168.81.112
- display: ip.addr == 192.168.81.112
- capture: host 192.168.81.112

Example **exclude RDP filter**
- display: !(tcp.port == 3389)
- capture: not port 3389

Example **only TCP ACK packets**
- display: tcp.flags.ack == 1
- capture: tcp[13] & 16 == 16

## Graphs
RTT graph = latency
- Best to show latency issues, RTT shows changes/spikes over time.
Flow graph = visualize a conversation
- Best for viewing the sequence of a protocol exchange.
I/O graph = packets/sec or bytes/sec
- whole capture, a protocol, or specific filtered conversation

## Packet analysis - tshark
tshark essentials
- **-D** = list interfaces
- **-i 1** = capture on interface 1
- **-w file.pcap** = write capture
- **-r file.pcap** = read capture file
- **-a duration:30** = stop after 30 seconds
- **-b** = ring buffer
	- **-b duration:30** = start new capture file every 30 seconds
	- **-b files:10** = only keep 10 files total, overwrite oldest when full
	- **-b filesize:100000** = rotate when file hits that size
- **-s 128** = snaplen (capture first 128 bytes of each packet)
merge
- mergecap -w merged.pcap file1.pcap file2.pcap
- mergecap -w merged.pcap mblais*
editcap
- editcap -r in.pcap out.pcap 300-450
	- Start at packet #300 and end at packet #450 then copy only those into out.pcap.
	- This will include 300, 301...450. (same as the packet number column from wireshark)
	- The `-r` means to include raw packet data (keep the bytes in the output not just headers and metadata.)
	- If `-r` is not included then output everything EXCEPT packets 300-450.


Example:
- write to new file every 30 seconds = `tshark -i 1 -b duration:30 -w capture.pcap`

## Subnetting

/25
00000000-00000000-00000000-00000000
11111111-11111111-11111111-10000000
10000000
128
255.255.255.128

## VLSM
1. sort required networks by host count (largest to smallest)
2. pick smallest subnet that fits each
3. allocate from the base network in order
4. for each subnet write.
	1. network
	2. first usable
	3. last usable
	4. broadcast
	5. mask


## Practice Questions

Write display and capture filter for:
- “Only traffic involving 10.0.0.5”
- “Exclude RDP”
- “Only DNS”

Command line:
- Difference between -a duration:30 and -b duration:30
- What does `-s 128` do
- How to merge Lab* pcaps
- How to extract packets 200–400

Subnetting/VLSM:
- Quickly state hosts for /26, /27, /28, /30
- Given a base /24 and 3 subnet needs, allocate using VLSM