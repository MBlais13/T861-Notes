
Question 1

One of the purposes of the three-way handshake is to check that the recipient is listing on the port.

 True
 False



Question 2

Socket does not have to be a unique combination of IP address and port number on each host.

 True
 False



Question 3

A socket pair is the combination of the sender and receiver sockets.

 True
 False



Question 4

Which of the following TCP header fields is responsible for defining the receiver buffer size?

		
Acknowledgment Number

 		
Options

 		
Window Size

 		
Sequence Number



Question 5

Which of the following TCP header fields is used to confirm receipt of data and setup the next portion of the transmission?

		
Acknowledgment Number

 		
Window Size

 		
Options

 		
Sequence Number



Question 6

What is the order of a TCP teardown?

		
> FIN/ACK

< ACK

< FIN/ACK

> ACK 


 		
> SYN

< SYN, ACK

> ACK

 		
> FIN

< FIN, ACK

> FIN

 		
> SYN, ACK

< ACK

< SYN, ACK

> ACK



Question 7

Which of the following sockets will listen to all incoming connections on port 1337 from any IP address?

		
*:1337

 		
::1337

 		
*.*.*.*:1337

 		
0.0.0.0/0:1337



Question 8

Which of the following sockets will listen to all requests on port 80 on either IP 10.135.23.46 or 10.135.24.46?

		
10.135.*.46:80

 		
::80

 		
10.135.23.46:80, 10.135.24.46:80

 		
*:80



Question 9

What is the purpose of the network layer?

		
To control the timing and delivery of data across various medium.

 		
To allow communication between different networks.

 		
To deal with which applications receive the data on each host.

 		
To create temporary point to point connections between hosts.



Question 10

Which of the following IPv6 multicast addresses would be the destination address to the Neighbor Solicitation packet for IPv6 address of 2001:db8:1::2:3434?

		
ff02::1:ff00:3434

 		
ff02::1:ff02:3434 

 		
2001:db8:1::2:FF00

 		
2001:db8:1::2:3434



Question 11

What does media access control mean?

		
Creating temporary connections

 		
Control the availability of information on a network through various software and hardware controls like firewalls

 		
Controlling users ability to access information through various means of authentication, sometimes involves combining forms of authentication

 		
Managing access to network medium



Question 12

What is the byte pattern of the start frame delimiter (SFD)?  This is located at the end of the preamble.

		
10101010

 		
01010100

 		
11110000

 		
10101011



Question 13

Which of the following is true regarding the IPv6 header?

		
The size of the hardware address field is 8 bytes

 		
The size of the source IP address field is 16 bytes

 		
The size of the hardware address field is 6 bytes

 		
The size of the source IP address field is 4 bytes



Question 14

In a standard ARP request, what is the target hardware address set to?

		
The target's MAC address

 		
The sender's MAC address

 		
All zeroes

 		
All ones



Question 15

In a gratuitous ARP request, what is the target protocol address set to?

		
The target's IP address.

 		
The sender's IP address

 		
255.255.255.255

 		
0.0.0.0



Question 16

What size can the data field in an ethernet II frame can be? 

		
64 - 1565 bytes

 		
64 - 1500  bytes

 		
46 - 1564  bytes

 		
46 - 1500  bytes



Question 17

What is the time to live field used for in the IPv4 packet header?

		
Defines the lifetime of the packet measured in hops through routers

 		
Defines the lifetime of the packet measured in seconds since transmissions

 		
Defines the lifetime of the packet measured in hops through routers and switches

 		
Defines the lifetime of the packet measured in hops through the network layers



Question 18

Match the different types of network layer transmissions to their respective definitions.

	
Unicast

 	
Multicast

 	
Broadcast

 	
Anycast

A.	
Transmission between one host to another

B.	
Transmission from one host to any one host from a group of hosts

C.	
Transmission from one host to all hosts on the network

D.	
Transmission from one host to many hosts in a group



Question 19

Match the following WAN encapsulation services to their definitions.

	
Addressing

 	
Bit-level integrity check

 	
Delimitation

 	
Protocol Identification

A.	
These are checksums calculated before and after transmission to confirm no change in the message has occurred during transmission.

B.	
Data link frames require specific end-of-frame markers, each frame header and trailer must be distinct from its payload.

C.	
To uniquely identify each connection, used when a WAN link has more then two nodes that are involved in possible connections.

D.	
Method used to identify and differentiate between the different protocols that are used on a WAN



Question 20

Match the ICMP header fields to their respective definitions.

	
Type

 	
Code

 	
Checksum

 	
Variable

A.	
Used to describe the ICMP message based on the RFC specification

B.	
Used as a sub category definition based on the RFC specification

C.	
Used to ensure that the contents of the ICMP header and data are intact upon arrival

D.	
The portion that changes depending on what is required for the ICMP message



Question 21

Every device on the network knows the subnet mask configured on the router.

 True
 False



Question 22

The upper layer protocol descriptor for IPv4 is 0x0800.

 True
 False



Question 23

An ARP reply is sent as a broadcast.

 True
 False



Question 24

The logical link control is responsible for creating point-to-multi-point connections.

 True
 False



Question 25

The upper layer protocol descriptor for ARP is 0x86DD.

 True
 False



Question 26

The fragmentation of a packet is based on the maximum transmission unit size of the layer 2 data link protocol.

 True
 False



Question 27

Which of the following is true regarding UDP?

		
[] Allows for communication to other networks

 		
[] Controls communication across different medium

 		
[] Tracks and ensures segment delivery

 		
[] Connectionless

 		
[] Connection-oriented protocol

 		
[] Uses best effort to deliver segments



Question 28

Which of the following is true regarding TCP?

		
[] Uses best effort to deliver segments

 		
[] Connection-oriented protocol

 		
[] Tracks and ensures segment delivery

 		
[] Allows for communication to other networks

 		
[] Connectionless

 		
[] Controls communication across different medium



Question 29

Which of the following are true regarding port numbers?

		
1024-49151 are Registered ports ports and are controlled by ICANN 

 		
1024-49151 are Registered ports which are not control by ICANN but can be registered to prevent duplication

 		
49152-65535 are Dynamic ports and are controlled by ICANN

 		
0-1023 are Well Known ports which are not control by ICANN but can be registered to prevent duplication 

 		
0-1023 are Well Known ports and are controlled by ICANN

 		
49152-65535 are Dynamic ports and are used as temporary or private port numbers

 		
49152-65535 are Registered ports which are not control by ICANN but can be registered to prevent duplication

 		
1024-49151 are Well Known ports and are controlled by ICANN

 		
0-1023 are Dynamic ports and are used as temporary or private port numbers



Question 30

There is no option to request your previous IP address in DHCP.

 True
 False



Question 31

SMTP deals with both transmitting mail messages to other users on the same domain as well as to other mail domains.

 True
 False



Question 32

You do not have to have MX records in your DNS server in order to  have a globally available email server.

 True
 False



Question 33

Which of the following is not a valid HTTP method?

		
DELETE

 		
PUT

 		
UPDATE

 		
GET



Question 34

What is used to describe the email and HTTP traffic content?

		
multipart/alternative

 		
multipart/related

 		
Mimetypes

 		
base64



Question 35

When a DHCP Discover is sent out what is the source and destination IP address?

		
S: The first 4 bytes of the MAC address

D: 255.255.255.255

 		
S: The previous IP address of the computer or 169.0.0.1 if there was no previous IP address

D: The default gateway of the network

 		
S: 0.0.0.0

D: 255.255.255.255

 		
S: 224.0.0.2

D: 224.0.0.255



Question 36

Which of the following was not one of the original top level domains?

		
.net

 		
.io

 		
.com

 		
.me



Question 37

When are recursive DNS lookups a good idea?

		
If the initial record is an MX to lookup the root of the domain

 		
If the initial record is a CNAME

 		
If the initial record is TXT it should follow the TXT record until it finally gets an IP address

 		
If the only available record is AAAA



Question 38

Which of the following is valid base64 (not including the trailing =)?

		
234AVC234abd???

 		
9832475kasaSDFSj;934895aksdfj

 		
aDsdfv234///asdf3234dSD+

 		
asd|lasdfjwern//++


Question 39

What is the top level domain of "www.youtube.goog"?

		
www

 		
goog

 		
. (period for root)

 		
youtube



Question 40

What port does DNS operate on?

		
43

 		
53

 		
453

 		
35



